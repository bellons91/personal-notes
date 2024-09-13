# Azure APIM policies

## Struttura base

Le policy sono gestite in 4 parti:

```xml
<policies>
    <inbound>
        <base />
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
    <on-error>
        <base />
    </on-error>
</policies>
```

- `inbound` trasforma i dati in input
- `backend` indica il sistema da chiamare dietro APIM
- `outbound` trasforma i dati in output
- `on-error` si occupa degli errori

## Come creare e utilizzare una variabile

Posso creare delle variabili usando `set-variable`

```xml
<set-variable name="listVariable" value="abc" />
```

e utilizzarle accedendo all'oggetto `context`, usando la sintassi `@(expr)`.

```xml
<nodo qualcosa="@($"{context.Variables["listVariable"]}")" >
```

## Come creare e utilizzare fragment

I fragment sono definiti sotto Policy fragments (nella blade a sx).

```xml
<fragment>
    <!-- Retrieve variables from key vault -->
    <set-variable name="clientId" value="@($"{{ClientId}}")" />
    <set-variable name="clientSecret" value="@($"{{ClientSecret}}")" />
    <!-- Retrieve bearer token -->
    <send-request mode="new" response-variable-name="tokenResponse" timeout="20" ignore-error="true">
        <set-url>la mia url</set-url>
        <set-method>POST</set-method>
        <set-header name="Content-Type" exists-action="override">
            <value>application/x-www-form-urlencoded</value>
        </set-header>
        <set-body>@($"client_id={context.Variables["clientId"]}&client_secret={context.Variables["clientSecret"]}&grant_type=client_credentials")</set-body>
    </send-request>
</fragment>
```

Posso poi utilizzare il fragment includendolo cosí:

```xml
<include-fragment fragment-id="ddlDaToken" />
```

## Come accedere ai dati delle request

Posso accedere all'oggetto `context`, in C#, per eseguire operazioni sui dati in input.

```xml
 <set-variable name="listVariable" value="@{
    var endpoint = context.Request.MatchedParameters["endpoint"].ToString();
    return string.Join("/", endpoint.Split('/'));
}" />

```

## Creare o fare override di un header

Nella policy di `inbound`, posso creare o fare override di un HTTP header:

```xml
<set-header name="Content-Type" exists-action="override">
    <value>application/json</value>
</set-header>
```

Il valore puó essere anche calcolato accedendo al contesto:

```xml
<set-header name="Authorization" exists-action="override">
    <value>@("Bearer " + ((IResponse)context.Variables["tokenResponse"]).Body.As<JObject>()["access_token"].ToString())</value>
</set-header>
```

## Aggiungere un certificato

Una volta che ho il thumbprint del certificato, posso utilizzarlo cosí

```xml
<authentication-certificate thumbprint="44EA9376C0BD3BDDD59B7Aqualcosaqualcosa" />
```

## Definisci rewrite url

Da capire:

```xml
<rewrite-uri template="@($"{context.Variables["listVariable"]}")" copy-unmatched-params="true" />
```

## Definisci CORS

```xml
<cors allow-credentials="true">
    <allowed-origins>
        <origin>http://localhost:4200</origin>
        <origin>https://localhost:4200</origin>
        <origin>https://salesapp-bf.enigaseluce.com</origin>
        <origin>https://egl-bf-b1.crm4.dynamics.com</origin>
        <origin>https://salesapp-bft1.enigaseluce.com</origin>
    </allowed-origins>
    <allowed-methods>
        <method>GET</method>
        <method>POST</method>
    </allowed-methods>
    <allowed-headers>
        <header>*</header>
    </allowed-headers>
    <expose-headers>
        <header>*</header>
    </expose-headers>
</cors>
```

## Definire il body di ritorno

```xml
<inbound>
    <base />
    <return-response>
        <set-status code="200" reason="OK" />
        <set-header name="Content-Type" exists-action="override">
            <value>application/json</value>
        </set-header>
        <set-body>
        {
            "Header": 
            {
                "Response":
                {
                    "Codice": "200",
                    "Descrizione": "Elaborazione avvenuta con successo",
                    "Tipo": "Info"
                }
            }       
        }
</set-body>
    </return-response>
</inbound>
```

Se il body é dinamico, bisogna usare il **liquid template**:

```xml
<return-response>
    <set-status code="200" reason="OK" />
    <set-header name="Content-Type" exists-action="override">
        <value>application/json</value>
    </set-header>
    <set-body template="liquid">
    {  
        "result": "001",
        "status": "Success",
        "response": {
            "tipoMisuratore": "{{context.Request.Headers['X-Expected-value']}}"
        }
    }
    </set-body>
</return-response>    
```

## Come leggere il valore di un header nella request

Ci sono due modi per leggere il valore di un header nella request.

O usi le parentesi quadre, ma cosí facendo ottieni l'array dei valori dei valori ricevuti in input

```xml
context.Request.Headers['X-Expected-value']
```

oppure usi `GetValueOrDefault`, specificando il valore da gestire nel caso in cui quell'header non sia stato passato in input.

```xml
 <when condition="@(context.Request.Headers.GetValueOrDefault("X-Expected-value", "") == "")">
```

## Switch-case

Si possono gestire diversi blocchi come se fossero switch-case:

Le keyword chiave sono `choose`, `when` e `otherwise`.

```xml
<choose>
    <when condition="@(context.Request.Headers.GetValueOrDefault("X-Expected-value", "") == "")">
        
    </when>
    <otherwise>
        
    </otherwise>
</choose>
```

## Fragment custom utili

### TraceOriginalPayloadWithoutSerialization

Logga cosa questa request ha ricevuto in input.

```xml
<fragment>
 <trace source="@(context.Operation.Id)" severity="information">
  <message>
            @{
                var body =  context.Request?.Body?.As<string>(preserveContent: true);

                var headers = context.Request?.Headers;
                Dictionary<string, string> contextProperties = new Dictionary<string, string>();
                foreach (var h in headers) {
                    contextProperties.Add(string.Format("{0}", h.Key), String.Join(", ", h.Value));
                }

                var requestLogMessage = new {
                    Headers = contextProperties,
                    Body = body
                };
                return string.Format("Input Request: {0}", JsonConvert.SerializeObject(requestLogMessage));
            }
        </message>
  <metadata name="Request" value="Original Payload and Headers Without Serialization" />
 </trace>
</fragment>
```

### SetAndTraceTransformedRequest

Trasforma la request iniziale (!!!!) e logga il suo contentuto.

```xml
<fragment>
 <set-body>@{
                return context.Variables.GetValueOrDefault<string>("transformedRequest");
        }</set-body>
 <trace source="@(context.Operation.Id)" severity="information">
  <message>@(String.Format("Transformed Request: \n {0}", context.Variables["transformedRequest"]))</message>
  <metadata name="TransactionId" value="@(context.Variables["transactionId"] as string)" />
  <metadata name="Request" value="Transformed Request" />
 </trace>
</fragment>
```

### TraceBackendPayload

Logga cosa il servizio di backend ha restituito.

```xml
<fragment>
 <trace source="@(context.Operation.Id)" severity="information">
  <message>Checked backend response body.</message>
  <metadata name="TransactionId" value="@(context.Variables["transactionId"] as string)" />
 </trace>
 <!--<set-variable name="backendPayload" value="@(context.Response.Body.As<JObject>())" />-->
 <trace source="@(context.Operation.Id)" severity="information">
    <message>
        @{
            var body =  context.Response?.Body?.As<string>(preserveContent: true);

            var headers = context.Response?.Headers;
            Dictionary<string, string> contextProperties = new Dictionary<string, string>();
            foreach (var h in headers) {
                contextProperties.Add(string.Format("{0}", h.Key), String.Join(", ", h.Value));
            }

            var responseLogMessage = new {
                Headers = contextProperties,
                Body = body
            };
            return string.Format("Backend Response: {0}", JsonConvert.SerializeObject(responseLogMessage ));
        }
    </message>
  <metadata name="TransactionId" value="@(context.Variables["transactionId"] as string)" />
  <metadata name="Response" value="Backend Payload with Headers" />
 </trace>
</fragment>
```

### TraceServiceErrors

Logga i messaggi di errore

```xml
<fragment>
 <trace source="@(context.Operation.Id)" severity="error">
  <message>@(String.Format("Errore nella logica del servizio: \n {0}", context.LastError.Message.ToString()))</message>
  <metadata name="TransactionId" value="@(context.Variables["transactionId"] as string)" />
  <metadata name="Service Error" value="Errore nella logica del servizio" />
 </trace>
</fragment>
```
