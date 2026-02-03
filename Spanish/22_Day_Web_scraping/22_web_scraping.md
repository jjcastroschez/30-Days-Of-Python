<div align="center">
  <h1> 30 Días de Python: Día 22 - Web scraping </h1>
  <a class="header-badge" target="_blank" href="https://www.linkedin.com/in/asabeneh/">
  <img src="https://img.shields.io/badge/style--5eba00.svg?label=LinkedIn&logo=linkedin&style=social">
  </a>
  <a class="header-badge" target="_blank" href="https://twitter.com/Asabeneh">
  <img alt="Twitter Follow" src="https://img.shields.io/twitter/follow/asabeneh?style=social">
  </a>

<sub>Autor:
<a href="https://www.linkedin.com/in/asabeneh/" target="_blank">Asabeneh Yetayeh</a><br>
<small> Segunda edición: julio de 2021</small>
</sub>
</div>

[<< Día 21](../21_Day_Classes_and_objects/21_classes_and_objects.md) | [Día 23 >>](../23_Day_Virtual_environment/23_virtual_environment.md)

![30DaysOfPython](../../images/30DaysOfPython_banner3@2x.png)

- [📘 Día 22](#-día-22)
  - [Web scraping con Python](#web-scraping-con-python)
    - [¿Qué es el web scraping?](#qué-es-el-web-scraping)
  - [💻 Ejercicios: Día 22](#-ejercicios-día-22)

# 📘 Día 22

## Web scraping con Python

### ¿Qué es el web scraping?

Internet está lleno de datos que pueden utilizarse para distintos fines. Para recopilar esos datos necesitamos saber cómo extraerlos de sitios web.

El web scraping es el proceso de extraer y recopilar datos de sitios web y almacenarlos en una máquina local o en una base de datos.

En esta sección usaremos los paquetes requests y BeautifulSoup (versión 4).

Para empezar necesitas _requests_,_beautifulsoup4_ y un _sitio web_:

```sh
pip install requests
pip install beautifulsoup4
```

Para hacer scraping necesitas conocimientos básicos de etiquetas HTML y selectores CSS. Usamos etiquetas HTML,clases y/o IDs para localizar contenido en la página.
Importemos requests y BeautifulSoup:

```py
import requests
from bs4 import BeautifulSoup
```

Declaremos una variable url con el sitio que queremos scrapear:

```py
import requests
from bs4 import BeautifulSoup
url = 'https://archive.ics.uci.edu/ml/datasets.php'

# Usamos requests.get para obtener datos de la URL
response = requests.get(url)
# Comprobar el estado
status = response.status_code
print(status) # 200 indica éxito
```

```sh
200
```

Parsear el contenido con BeautifulSoup:

```py
import requests
from bs4 import BeautifulSoup
url = 'https://archive.ics.uci.edu/ml/datasets.php'

response = requests.get(url)
content = response.content # obtenemos todo el contenido del sitio
soup = BeautifulSoup(content, 'html.parser') # BeautifulSoup nos permite parsear el HTML
print(soup.title) # <title>UCI Machine Learning Repository: Data Sets</title>
print(soup.title.get_text()) # UCI Machine Learning Repository: Data Sets
print(soup.body) # muestra el cuerpo completo de la página
print(response.status_code)

tables = soup.find_all('table', {'cellpadding':'3'})
# Localizamos tablas cuyo atributo cellpadding tenga el valor 3
# Podemos usar id, class o etiquetas HTML para seleccionar elementos; consulta la documentación de BeautifulSoup para más información
table = tables[0] # el resultado es una lista; tomamos el primer elemento
for td in table.find('tr').find_all('td'):
    print(td.text)
```

Si ejecutas este código verás que la extracción está incompleta.Puedes continuar para completarla,ya que forma parte del ejercicio 1.
Consulta la documentación de BeautifulSoup para más detalles: https://www.crummy.com/software/BeautifulSoup/bs4/doc/#quick-start

🌕 Vas por muy buen camino.Solo te faltan ocho días para alcanzar una meta impresionante.Ahora haz los ejercicios para practicar.

## 💻 Ejercicios: Día 22

1. Raspa el siguiente sitio y guarda los datos como un archivo JSON (url = 'http://www.bu.edu/president/boston-university-facts-stats/').
2. Extrae las tablas de esta URL (https://archive.ics.uci.edu/ml/datasets.php) y conviértelas a un archivo JSON.
3. Raspa la tabla de presidentes y guarda los datos como JSON (https://en.wikipedia.org/wiki/List_of_presidents_of_the_United_States).Esta tabla no está muy bien estructurada,por lo que la extracción puede llevar tiempo.

🎉 ¡Felicidades!🎉

[<< Día 21](../21_Day_Classes_and_objects/21_classes_and_objects.md) | [Día 23 >>](../23_Day_Virtual_environment/23_virtual_environment.md)