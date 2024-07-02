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
