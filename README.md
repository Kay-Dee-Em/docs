# SQL RadioAI

## Wprowadzenie
SQL (Structured Query Language) to język używany do komunikacji z bazami danych. Pozwala na tworzenie, modyfikowanie oraz pobieranie danych.

## Podstawowe polecenia SQL

### 1. SELECT
Służy do wybierania danych z bazy.

```sql
SELECT kolumna1, kolumna2 FROM nazwa_tabeli;
```

### 2. WHERE
Dodaje warunki filtrowania danych.

```sql
SELECT kolumna1, kolumna2 
FROM nazwa_tabeli 
WHERE warunek;
```

### 3. ORDER BY
Sortuje wyniki według jednej lub więcej kolumn.

```sql
SELECT kolumna1, kolumna2 
FROM nazwa_tabeli 
ORDER BY kolumna1 ASC;
```

### 4. GROUP BY
Grupuje wyniki na podstawie jednej lub więcej kolumn.

```sql
SELECT kolumna1, COUNT(*) 
FROM nazwa_tabeli 
GROUP BY kolumna1;
```

### 5. IN
Pozwala sprawdzić, czy wartość kolumny znajduje się w określonym zbiorze wartości.

```sql
SELECT kolumna1, kolumna2 
FROM nazwa_tabeli 
WHERE kolumna1 IN ('wartość1', 'wartość2', 'wartość3');
```

### 6. LIKE
Umożliwia wyszukiwanie wzorców w danych tekstowych.

```sql
SELECT kolumna1, kolumna2 
FROM nazwa_tabeli 
WHERE kolumna1 LIKE 'wzorzec%';
```

### 7. LIMIT
Ogranicza liczbę zwróconych rekordów.

```sql
SELECT kolumna1, kolumna2 
FROM nazwa_tabeli 
ORDER BY kolumna1 DESC 
LIMIT 10;
```

### 8. DISTINCT
Usuwa duplikaty z wyników.

```sql
SELECT DISTINCT kolumna1 
FROM nazwa_tabeli;
```

### 9. JOIN
Łączy dane z dwóch tabel na podstawie powiązanej kolumny.

```sql
SELECT a.kolumna1, u.kolumna2, u.kolumna3 
FROM nazwa_tabeli1 a 
JOIN nazwa_tabeli2 u 
  ON a.kolumna1 = u.kolumna2;
```

### 10. AVG() i SUM()
Używa funkcji agregujących do obliczeń.

```sql
SELECT AVG(kolumna1) AS srednia_wartosc, SUM(kolumna1) AS suma_wartosci 
FROM nazwa_tabeli 
WHERE kolumna4 = wartosc;
```

### 11. HAVING
Filtruje wyniki po agregacji danych.

```sql SELECT kolumna1, COUNT(*) as count 
FROM nazwa_tabeli 
GROUP BY kolumna1 
HAVING COUNT(*) > wartosc;
```

### 12. UNION
Łączy wyniki dwóch lub więcej zapytań o takich samych kolumnach.

```sql
SELECT kolumna1 FROM nazwa_tabeli1 
UNION 
SELECT kolumna1 FROM nazwa_tabeli2;
```

### 13. CASE
Dodaje logikę warunkową do zapytań.

```sql
SELECT kolumna1,
       CASE 
           WHEN kolumna1 > wartosc1 THEN wartosc3
           WHEN kolumna1 > wartosc2 THEN wartosc4
           ELSE wartosc5
       END AS kolumna2
FROM nazwa_tabeli;
```

### 14. BETWEEN
Sprawdza czy wartość mieści się w zadanym zakresie.

```sql
SELECT kolumna1 
FROM nazwa_tabeli 
WHERE kolumna1 BETWEEN wartosc1 AND wartosc2;
```

### 15. IS NULL
Sprawdza czy wartość jest pusta.

```sql
SELECT kolumna1 
FROM nazwa_tabeli 
WHERE kolumna1 IS NULL;
```

## Przykładowe Zapytania

### Przykład SELECT z WHERE

```sql
SELECT title, content, category, radio
FROM nazwa_tabeli 
WHERE category = 'biznes' AND radio <> 'se';
```

### Przykład SELECT z ORDER BY

```sql
SELECT * 
FROM articles_article 
ORDER BY deadline DESC;
```

### Przykład SELECT z GROUP BY

```sql
SELECT category, COUNT(*) AS no_articles 
FROM articles_article 
GROUP BY category;
```

### Przykład SELECT z IN

```sql
SELECT title, content, category, radio
FROM articles_program 
WHERE
radio IN ('se', 'eska'); 
AND category NOT IN ('sport', 'dziennik', 'pilne');
```

### Przykład SELECT z LIKE

```sql
SELECT title, content, category 
FROM articles_article 
WHERE 
title LIKE '%2025_01_18%'
AND title NOT LIKE '%2025_01_18_00%';
```

### Przykład z LIMIT

```sql
SELECT title, content, category
FROM articles_article
WHERE category = 'biznes' OR category = 'sport' 
ORDER BY date_posted DESC, title ASC
LIMIT 10;
```

### Przykład z DISTINCT

```sql
SELECT DISTINCT category 
FROM articles_article;
```

### Przykład z JOIN

```sql
SELECT a.title, a.content, g.grade 
FROM articles_article a 
JOIN articles_gradearticle g 
  ON a.id = g.article_id;
```

### Przykład z AVG i SUM

```sql
SELECT AVG(initial_length) AS avg_length, SUM(initial_length) AS sum_length 
FROM articles_article 
WHERE initial_length > 30;
```

### Przykład z HAVING

```sql SELECT category, COUNT(*) as count 
FROM articles_article 
GROUP BY category 
HAVING COUNT(*) > 5;
```

### Przykład z UNION

```sql
SELECT title FROM articles_article 
UNION 
SELECT title FROM articles_program;
```

### Przykład z CASE

```sql
SELECT title,
       CASE 
           WHEN initial_length > 30 THEN 'Długi'
           WHEN initial_length > 20 THEN 'Średni'
           ELSE 'Krótki'
       END AS audio_length
FROM articles_article;
```

### Przykład z BETWEEN

```sql
SELECT title, deadline 
FROM articles_article 
WHERE deadline BETWEEN '2024-01-01' AND '2024-12-31';
```

### Przykład z IS NULL/IS NOT NULL

```sql
SELECT title, radio 
FROM articles_article 
WHERE title IS NOT NULL
AND radio IS NULL;
```


## Opis Parametrów

- **SELECT**: Wybiera kolumny do wyświetlenia.
- **FROM**: Określa tabelę, z której pobierane są dane.
- **WHERE**: Ustawia warunki filtrowania rekordów.
- **ORDER BY**: Sortuje wyniki według wskazanych kolumn (**ASC** - rosnąco, **DESC** - malejąco).
- **GROUP BY**: Grupuje wyniki na podstawie określonych kolumn.
- **COUNT(*)**: Liczy liczbę rekordów w grupie.
- **AS**: Nadaje alias (przyjazną nazwę) kolumnie lub wyrażeniu.
- **IN**: Sprawdza, czy wartość znajduje się w zbiorze wartości.
- **LIKE**: Wyszukuje wzorce w danych tekstowych.
- **LIMIT**: Ogranicza liczbę zwróconych rekordów.
- **DISTINCT**: Usuwa duplikaty z wyników.
- **JOIN**: Łączy dane z różnych tabel na podstawie powiązanych kolumn (dodaje kolumny).
- **AVG()**: Oblicza średnią wartość.
- **SUM()**: Oblicza sumę wartości.
- **HAVING**: Filtruje wyniki po agregacji danych.
- **UNION**: Łączy wyniki dwóch lub więcej zapytań (dodaje wiersze).
- **CASE**: Dodaje logikę warunkową do zapytań.
- **BETWEEN**: Sprawdza, czy wartość mieści się w zadanym zakresie.
- **IS NULL/IS NOT NULL**: Sprawdza, czy wartość jest/nie jest pusta.

## Przykład Kompletny

Załóżmy, że masz tabelę `articles_program` z kolumnami `title`, `category`, `kategoria`, `date_posted`.

```sql
SELECT title, category, date_posted
FROM articles_program 
WHERE category = 'biznes' 
AND radio IN ('se', 'eska')
AND date_posted BETWEEN '2024-01-01' AND '2024-12-31'
ORDER BY date_posted DESC, category ASC
LIMIT 5;
```

- **SELECT titie, category**: Wybiera kolumny `title`, `category` i `date_posted`.
- **FROM programy**: Z tabeli `articles_program`.
- **WHERE category = 'biznes'**: Filtruje programy z kategorii 'biznes'.
- **AND radio IN ('se', 'eska')**: Filtruje programy z radia 'eska' lub 'se'.
- **AND date_posted BETWEEN '2024-01-01' AND '2024-12-31'**: Filtruje programy z deadlinem pomiędzy '2024-01-01' a '2024-12-31'
- **ORDER BY date_posted DESC, category ASC**: Sortuje wyniki według daty opublikowania w kolejności malejącej, a następnie według kategorii w kolejności rosnącej.
- **LIMIT 5**: Zwraca tylko pierwsze 5 rekordów.

