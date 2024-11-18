consulta #1
```sql
#Encuentra los países que tienen un idioma oficial.
select * from countrylenguage;
select distinct countrycode
from countrylenguage
where IsOfficial = 'T'; 
```
consulta #2
```sql
#Lista los países que tienen más de un idioma oficial.
from countrylenguage
where IsOfficial= 'T'
group by countrycode
having count(*)>1;
```

consulta #3
```sql
# Encuentra los países que tienen el mismo continente que Japón.
SELECT c.Name
FROM Country c
JOIN CountryLanguage cl ON c.Code = cl.CountryCode
WHERE c.Continent = (
    SELECT Continent
    FROM Country
    WHERE Name = 'Japan'
);
```
consulta #4
```sql
#Encuentra las ciudades que tienen población mayor a 5 millones y están en América del Sur.
SELECT ci.Name
FROM City ci
JOIN Country co ON ci.CountryCode = co.Code
WHERE ci.Population > 5000000
  AND co.Continent = 'South America';
```

consulta #5
```sql
#Encuentra los países que no tienen ningún idioma oficial.
SELECT c.Code
FROM Country c
WHERE c.Code NOT IN (
    SELECT cl.CountryCode
    FROM CountryLanguage cl
    WHERE cl.IsOfficial = 'T'
);
```
consulta #6
```sql
#Encuentra los idiomas que son oficiales en al menos dos países.
SELECT cl.Language
FROM CountryLanguage cl
WHERE cl.IsOfficial = 'T'
GROUP BY cl.Language
HAVING COUNT(DISTINCT cl.CountryCode) >= 2;
```

consulta #7
```sql
# Lista los países y su capital.
SELECT c.Name AS CountryName, ci.Name AS CapitalName
FROM Country c
JOIN City ci ON c.Capital = ci.ID;
```

consulta #8
```sql
#Encuentra los países que tienen una población mayor que Alemania.
SELECT c.Name
FROM Country c
WHERE c.Population > (
    SELECT Population
    FROM Country
    WHERE Name = 'Germany'
);
```

consulta #9
```sql
#Encuentra los idiomas oficiales de Europa.
SELECT DISTINCT cl.Language
FROM Country c
JOIN CountryLanguage cl ON c.Code = cl.CountryCode
WHERE c.Continent = 'Europe' AND cl.IsOfficial = 'T';
```

consulta #10
```sql
# Encuentra los países sin ciudades registradas en la tabla City.
SELECT c.Code
FROM Country c
WHERE c.Code NOT IN (
    SELECT ci.CountryCode
    FROM City ci
);
```

consulta #11
```sql
#Muestra la población total de cada continente.
SELECT Continent, SUM(Population) AS TotalPopulation
FROM Country
GROUP BY Continent;
```

consulta #12
```sql
# Encuentra los países en los que la esperanza de vida es menor al promedio global.
SELECT Name
FROM Country
WHERE LifeExpectancy < (
    SELECT AVG(LifeExpectancy)
    FROM Country
);
```

consulta #13
```sql
#Encuentra los países en Asia sin idioma oficial registrado.
SELECT c.Code
FROM Country c
WHERE c.Continent = 'Asia'
AND c.Code NOT IN (
    SELECT cl.CountryCode
    FROM CountryLanguage cl
    WHERE cl.IsOfficial = 'T'
);
```

consulta #14
```sql
#Lista los idiomas que son oficiales en países con esperanza de vida mayor a 80.
SELECT DISTINCT cl.Language
FROM Country c
JOIN CountryLanguage cl ON c.Code = cl.CountryCode
WHERE c.LifeExpectancy > 80 AND cl.IsOfficial = 'T';
```

consulta #15
```sql
#Encuentra los países con más de 10 ciudades en la tabla City.
SELECT CountryCode
FROM City
GROUP BY CountryCode
HAVING COUNT(*) > 10;
```

consulta #16
```sql
#Qué países tienen una población mayor a 50 millones
SELECT Name 
FROM Country 
WHERE Population > 50000000;
```

consulta #17
```sql
#Qué ciudades tienen una población mayor a 1 millón
SELECT Name 
FROM City 
WHERE Population > 1000000;
```

consulta #18
```sql
# Qué idiomas se hablan en más del 50% de la población de su país
SELECT Language 
FROM CountryLanguage 
WHERE Percentage > 50;
```

consulta #19
```sql
#Qué países tienen una expectativa de vida mayor a 75 años
SELECT Name 
FROM Country 
WHERE LifeExpectancy > 75;
```

consulta #20
```sql
#Qué ciudades son capitales
SELECT City.Name 
FROM City 
JOIN Country ON City.ID = Country.Capital;
```

consulta #21
```sql
#Qué países tienen más de 5 ciudades registradas en la base de datos
SELECT CountryCode, COUNT(*) AS CityCount 
FROM City 
GROUP BY CountryCode 
HAVING CityCount > 5;
```

consulta #22
```sql
#Cuál es la ciudad más poblada de cada país
SELECT CountryCode, Name, MAX(Population) AS MaxPopulation 
FROM City 
GROUP BY CountryCode;
```

consulta #23
```sql
#Qué países tienen un producto interno bruto mayor a 1 billón
SELECT Name 
FROM Country 
WHERE GNP > 1000000;
```

consulta #24
```sql
# Qué idiomas se hablan en los países con más de 100 millones de habitantes
SELECT DISTINCT CountryLanguage.Language 
FROM CountryLanguage 
JOIN Country ON CountryLanguage.CountryCode = Country.Code 
WHERE Country.Population > 100000000;
```

consulta #25
```sql
# Qué países tienen ciudades que suman más de 10 millones de habitantes en total
SELECT CountryCode, SUM(Population) AS TotalPopulation 
FROM City 
GROUP BY CountryCode 
HAVING TotalPopulation > 10000000;
```
