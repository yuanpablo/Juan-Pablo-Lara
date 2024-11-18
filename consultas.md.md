consulta #1
```sql
#Encuentra los países que tienen un idioma oficial.
select distinct countrycode
from countrylenguage
where IsOfficial = 'T'; 
```
![](./imagenes/numero1.png?raw=true)
consulta #2
```sql
#Lista los países que tienen más de un idioma oficial.
Select*from countrylenguage
where IsOfficial= 'T'
group by countrycode
having count(*)>1;
```
![](./imagenes/numero2.png?raw=true)
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
![](./imagenes/numero3.png?raw=true)
consulta #4
```sql
#Encuentra las ciudades que tienen población mayor a 5 millones y están en América del Sur.
SELECT ci.Name
FROM City ci
JOIN Country co ON ci.CountryCode = co.Code
WHERE ci.Population > 5000000
  AND co.Continent = 'South America';
```
![](./imagenes/numero4.png?raw=true)
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
![](./imagenes/nuemro5.png?raw=true)
consulta #6
```sql
#Encuentra los idiomas que son oficiales en al menos dos países.
SELECT cl.Language
FROM CountryLanguage cl
WHERE cl.IsOfficial = 'T'
GROUP BY cl.Language
HAVING COUNT(DISTINCT cl.CountryCode) >= 2;
```
![](./imagenes/numero6.png?raw=true)
consulta #7
```sql
# Lista los países y su capital.
SELECT c.Name AS CountryName, ci.Name AS CapitalName
FROM Country c
JOIN City ci ON c.Capital = ci.ID;
```
![](./imagenes/numero7.png?raw=true)
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
![](./imagenes/numero8.png?raw=true)
consulta #9
```sql
#Encuentra los idiomas oficiales de Europa.
SELECT DISTINCT cl.Language
FROM Country c
JOIN CountryLanguage cl ON c.Code = cl.CountryCode
WHERE c.Continent = 'Europe' AND cl.IsOfficial = 'T';
```
![](./imagenes/numero9.png?raw=true)
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
![](./imagenes/numero10.png?raw=true)
consulta #11
```sql
#Muestra la población total de cada continente.
SELECT Continent, SUM(Population) AS TotalPopulation
FROM Country
GROUP BY Continent;
```
![](./imagenes/numero11.png?raw=true)
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
![](./imagenes/numero12.png?raw=true)
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
![](./imagenes/numero13.png?raw=true)
consulta #14
```sql
#Lista los idiomas que son oficiales en países con esperanza de vida mayor a 80.
SELECT DISTINCT cl.Language
FROM Country c
JOIN CountryLanguage cl ON c.Code = cl.CountryCode
WHERE c.LifeExpectancy > 80 AND cl.IsOfficial = 'T';
```
![](./imagenes/numero14.png?raw=true)
consulta #15
```sql
#Encuentra los países con más de 10 ciudades en la tabla City.
SELECT CountryCode
FROM City
GROUP BY CountryCode
HAVING COUNT(*) > 10;
```
![](./imagenes/numero15.png?raw=true)
consulta #16
```sql
#Qué países tienen una población mayor a 50 millones
SELECT Name 
FROM Country 
WHERE Population > 50000000;
```
![](./imagenes/numero16.png?raw=true)
consulta #17
```sql
#Qué ciudades tienen una población mayor a 1 millón
SELECT Name 
FROM City 
WHERE Population > 1000000;
```
![](./imagenes/numero17.png?raw=true)
consulta #18
```sql
# Qué idiomas se hablan en más del 50% de la población de su país
SELECT Language 
FROM CountryLanguage 
WHERE Percentage > 50;
```
![](./imagenes/numero18.png?raw=true)
consulta #19
```sql
#Qué países tienen una expectativa de vida mayor a 75 años
SELECT Name 
FROM Country 
WHERE LifeExpectancy > 75;
```
![](./imagenes/numero19.png?raw=true)
consulta #20
```sql
#Qué ciudades son capitales
SELECT City.Name 
FROM City 
JOIN Country ON City.ID = Country.Capital;
```
![](./imagenes/numero20.png?raw=true)
consulta #21
```sql
#Qué países tienen más de 5 ciudades registradas en la base de datos
SELECT CountryCode, COUNT(*) AS CityCount 
FROM City 
GROUP BY CountryCode 
HAVING CityCount > 5;
```
![](./imagenes/numero21.png?raw=true)
consulta #22
```sql
#Cuál es la ciudad más poblada de cada país
SELECT CountryCode, Name, MAX(Population) AS MaxPopulation 
FROM City 
GROUP BY CountryCode;
```
![](./imagenes/numero22.png?raw=true)
consulta #23
```sql
#Qué países tienen un producto interno bruto mayor a 1 billón
SELECT Name 
FROM Country 
WHERE GNP > 1000000;
```
![](./imagenes/numero23.png?raw=true)
consulta #24
```sql
# Qué idiomas se hablan en los países con más de 100 millones de habitantes
SELECT DISTINCT CountryLanguage.Language 
FROM CountryLanguage 
JOIN Country ON CountryLanguage.CountryCode = Country.Code 
WHERE Country.Population > 100000000;
```
![](./imagenes/numero24.png?raw=true)
consulta #25
```sql
# Qué países tienen ciudades que suman más de 10 millones de habitantes en total
SELECT CountryCode, SUM(Population) AS TotalPopulation 
FROM City 
GROUP BY CountryCode 
HAVING TotalPopulation > 10000000;
```
![](./imagenes/numero25.png?raw=true)
