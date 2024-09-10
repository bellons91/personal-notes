---
tags: sql, tsql
---

# SQL/TSQL Cheatsheet

## Fare Count in SELECT

Si possono fare operazioni nella `SELECT` usando l'operatore `Count`.

> Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

```sql
SELECT
  Count(City) - Count(DISTINCT(City))
FROM
  Station
```

## Calcolare la lunghezza di una stringa

Si usa l'operatore `LEN`. Puó essere usato sia nella `SELECT` che nella `WHERE`.

```sql
SELECT
  TOP 1 City,
  LEN(City)
FROM
  STATION
ORDER BY
  LEN(City) DESC,
  City;
```

## Leggere una sottostringa

Usa l'operatore `SUBSTRING`, specificando la posizione del primo elemento (**in base 1**) e la lunghezza della sottostringa.

```sql
SELECT
  DISTINCT CITY
FROM
  Station
WHERE
  SUBSTRING (CITY, 1, 1) IN ('A', 'E', 'I', 'O', 'U')
```

Puoi partire dal fondo usando in `-`, ma considerando che le posizioni sono base 1. Per prendere gli ultimi 3 caratteri, usa `Len(nome_campo)-2`.

```sql
ORDER BY
  substring (Name, Len(Name) -2, 3),
  Id
```

## Selezionare item in base ad una regex

Usa l'operatore `LIKE`, con `%` come jolly, specificando una regex da seguire.

> Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters.

```sql
SELECT
  DISTINCT City
FROM
  station
WHERE
  City LIKE '[aeiou]%[aeiou]'
```

Usa l'operatore `^` per le negazioni:

> Query the list of CITY names from STATION that do not start with vowels.

```sql
SELECT
  DISTINCT city
FROM
  station
WHERE
  city LIKE '[^aeiou]%'
```

## SWITCH - CASE

Per fare switch bisogna definire il `CASE`, i vari `WHEN` col rispettivo `THEN`, il `ELSE` per il default, e concludere l'operazione con `END`.

> Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:
>
>
>Equilateral: It's a triangle with  sides of equal length.
>Isosceles: It's a triangle with  sides of equal length.
>Scalene: It's a triangle with  sides of differing lengths.
>Not A Triangle: The given values of A, B, and C don't form a triangle.

```sql
SELECT
  CASE
    WHEN A + B <= C
    OR A + C <= B
    OR B + C <= A THEN "Not A Triangle"
    WHEN A = B
    AND B = C THEN "Equilateral"
    WHEN A = B
    OR B = C
    OR A = C THEN "Isosceles"
    ELSE "Scalene"
  END
FROM
  TRIANGLES
```

## Subquery e referenze

Nel FROM posso definire delle sottoquery, dare un nome alla tabella restituita, e referenziarla al di fuori della query stessa.

```sql
SELECT
  TOP 1 MAX(VAL),
  COUNT(*)
FROM
  (
    SELECT
      months * salary AS VAL
    FROM
      Employee
  ) s
GROUP BY
  s.VAL
ORDER BY
  VAL DESC
```

Qui la subquery viene chiamata `s`, e si puó referenziare il suo campo VAL.
**E' necessario dare un nome alla subquery**.

## GroupBy e OrderBy

Puoi usare OrderBY per ordinare in base a quello che c'è in GroupBy.

Si ordina in base alla posizione del campo, quindi

```sql
Select *
from occupations
group by occupation 
order by 1
```

## Cast a tipo

Usa l'operatore `CAST`, specificando anche il tipo di destinazione.

```sql
CAST Salary AS integer
```

## Replace sottostringa

Usa l'operatore `REPLACE`, specificando la sottostringa da cercare e quella con cui sostituirla

```sql
REPLACE(Salary, '0', '')
```

Nota: la stringa di partenza non deve esser per forza una stringa. Puó anche essere un numero (come Salary), e funziona lo stesso.

## Arrotondare fino a una determinata cifra decimale

Se voglio arrotondare fino alla 4 cifra decimale, posso usare `CAST` specificando che converto il numero in `NUMERIC(a, b)`, dove `a` é il numero totale di cifre, mentre `b` é il numero di cifre decimali disponibili.

```sql
CAST(123,4567890 AS NUMERIC(12, 3)) # diventa 123,456
```

## Ottenere il valore in percentile di una query

Per ottenere il valore in un determinato percentile uso la funziona `percentile_cont`.

```sql
SELECT
  DISTINCT percentile_cont(0.5) WITHIN GROUP (
    ORDER BY
      LAT_N
  ) OVER()
FROM
  STATION
```

La query sopra prende tutti i valori di LAT_N presenti nella tabella Station, ne fa una partizione in base ai valori, poi prende il valore in percentile 0.5 e, tramite DISTINCT, ne restituisce un singolo valore.
