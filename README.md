# Les volcans et leurs éruptions significatives

Les volcans sont 


<iframe width="560" height="315" src="https://www.youtube.com/embed/CiHD5rDQdi8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Sommaire
1. [Présentation du jeu de données](#Jeudedonnees)
2. [Carte des éruptions significatives depuis -455]<a name="carte"></a>
3. [Liste des volcans connus à ce jour](#listeVolcan)
4. [Les différents types de volcan](#TypedeVolcan)
5. [Répartition des volcans selon l'indice d'explosivité volcanique](#IEV)



## Présentation du jeu de données <a name="Jeudedonnees"></a>

Le jeu de données utilisé afin d'étudier les volcans a été trouvé sur OpenDataSoft: 
>[Significant Volcanic Eruption Database](https://public.opendatasoft.com/explore/dataset/significant-volcanic-eruption-database/table/?flg=fr)

Ce jeu de données regroupe les "éruptions volcaniques significatives" qu'à connu notre monde. Pour être considérée comme une éruption significative, l'éruption doit répondre à différents critères:
* causer la mort 
* créer des dommages financiers
* Avoir un Indice d'Explosivité Volcanique de 6 ou plus
* Etre accompagner de tremblement de terre ou de tsunami

La production de cette base de données a été faite par les Centres nationaux d'information sur l'environnement et la licence appartient au domaine public américain. 

Le jeu de données, avant d'être exploitable, a dû être travaillé. Ainsi, la traduction du jeu de données a été faite, ainsi que la création de la colonne "date de l'éruption". 

Voici des extraits des modifications apportées: 

```sparql
[
  {
    "op": "core/column-rename",
    "oldColumnName": "Year",
    "newColumnName": "Année",
    "description": "Rename column Year to Année"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Month",
    "newColumnName": "Mois",
    "description": "Rename column Month to Mois"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Day",
    "newColumnName": "Jours",
    "description": "Rename column Day to Jours"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Volcano Name",
    "newColumnName": "Nom du volcan",
    "description": "Rename column Volcano Name to Nom du volcan"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Volcano Type",
    "newColumnName": "Type de volcan",
    "description": "Rename column Volcano Type to Type de volcan"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Country",
    "newColumnName": "Pays",
    "description": "Rename column Country to Pays"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Coordinates",
    "newColumnName": "Coordonées",
    "description": "Rename column Coordinates to Coordonées"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Volcanic Explosivity Index",
    "newColumnName": "Index d'explosivité volcanique",
    "description": "Rename column Volcanic Explosivity Index to Index d'explosivité volcanique"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Status",
    "newColumnName": "Statut",
    "description": "Rename column Status to Statut"
  },

```
```sparql
 "mode": "row-based"
    },
    "baseColumnName": "Année",
    "expression": "join ([coalesce(cells['Année'].value,'01'),coalesce(cells['Mois'].value,'01'),coalesce(cells['Jours'].value,'01')],'-')",
    "onError": "keep-original",
    "newColumnName": "Date de l'éruption",
    "columnInsertIndex": 2,
    "description": "Create column Date de l'éruption at index 2 based on column Année using expression join ([coalesce(cells['Année'].value,'01'),coalesce(cells['Mois'].value,'01'),coalesce(cells['Jours'].value,'01')],'-')"
  },
  {
    "op": "core/text-transform",
    "engineConfig": {
      "facets": [
        {
          "type": "range",
          "name": "Année",
          "expression": "value",
          "columnName": "Année",
          "from": -200,
          "to": 1300,
          "selectNumeric": false,
          "selectNonNumeric": true,
          "selectBlank": true,
          "selectError": true
        }
      ],
      "mode": "row-based"
    },
    "columnName": "Date de l'éruption",
    "expression": "value.toDate()",
    "onError": "keep-original",
    "repeat": false,
    "repeatCount": 10,
    "description": "Text transform on cells in column Date de l'éruption using expression value.toDate()"
  }
```


## Carte des éruptions significatives depuis -455<a name="carte"></a>

Les éruptions volcaniques sont visibles tout autour du globe. Nous pouvons voir ici que des zones sont, tout de même, plus touchées que d'autres par des explosions significatives. 

<iframe src="https://public.opendatasoft.com/explore/embed/dataset/significant-volcanic-eruption-database/map/?flg=fr&location=2,11.9211,-14.23828&basemap=jawg.light&dataChart=eyJxdWVyaWVzIjpbeyJjb25maWciOnsiZGF0YXNldCI6InNpZ25pZmljYW50LXZvbGNhbmljLWVydXB0aW9uLWRhdGFiYXNlIiwib3B0aW9ucyI6eyJmbGciOiJmciIsImJhc2VtYXAiOiJqYXdnLmxpZ2h0IiwibG9jYXRpb24iOiIyLDMuMTg5MzQsLTIuMjMifX0sImNoYXJ0cyI6W3siYWxpZ25Nb250aCI6dHJ1ZSwidHlwZSI6ImNvbHVtbiIsImZ1bmMiOiJBVkciLCJ5QXhpcyI6InllYXIiLCJzY2llbnRpZmljRGlzcGxheSI6dHJ1ZSwiY29sb3IiOiIjRkY1MTVBIn1dLCJ4QXhpcyI6InRzdSIsIm1heHBvaW50cyI6NTAsInNvcnQiOiIifV0sInRpbWVzY2FsZSI6IiIsImRpc3BsYXlMZWdlbmQiOnRydWUsImFsaWduTW9udGgiOnRydWV9&static=false&datasetcard=false&scrollWheelZoom=false" width="400" height="300" frameborder="0"></iframe>

## Liste des volcans connus à ce jour<a name="listeVolcan"></a>

Evidemment, toutes les éruptions ne sont pas significatives et par conséquents, tous les volcans ne sont pas répertoriés dans cette base de données. 
Vous pouvez, ici, découvrir tous les volcans existants ainsi que certaines de leurs caractéristiques (hauteur, localisation).

<iframe style="width: 80vw; height: 50vh; border: none;" src="https://query.wikidata.org/embed.html#%23%20Volcans%20%C3%A0%20travers%20le%20monde%0A%23defaultView%3AImageGrid%0ASELECT%20%3Fitem%20%3FitemLabel%20%3Fpic%20%3FlocalisationLabel%20%3Fcoordonnees%20%3Ftaille%20%3Fitemdescription%20%3FobservatoireLabel%0AWHERE%0A%7B%0A%3Fitem%20wdt%3AP31%20wd%3AQ8072%20.%0A%3Fitem%20wdt%3AP18%20%3Fpic%20.%0A%3Fitem%20wdt%3AP17%20%3Flocalisation%20.%0A%3Flocalisation%20wdt%3AP625%20%3Fcoordonnees%20.%0A%3Fitem%20schema%3Adescription%20%3Fitemdescription.%0A%20%20FILTER%28LANG%28%3Fitemdescription%29%20%3D%20%22fr%22%29%0A%3Fitem%20wdt%3AP3815%20%3Fobservatoire%0A%0AOPTIONAL%20%7B%3Fitem%20wdt%3AP2044%20%3Ftaille%7D%0A%20%20%20%20%20%20%20%20%20%7B%3Fitem%20wdt%3AP18%20%3Fpic%7D%0A%20%20%20%20%0A%0ASERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%2C%20fr%22%20%7D%0A%7D%0A%0A" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>


Pour visualiser cette galerie d'image, nous avons utiliser wikidata et son système de requête. La requête suivante a été utilisée: 


```sparql
# Volcans à travers le monde
#defaultView:ImageGrid
SELECT ?item ?itemLabel ?pic ?localisationLabel ?coordonnees ?taille ?itemdescription ?observatoireLabel
WHERE
{
?item wdt:P31 wd:Q8072 .
?item wdt:P18 ?pic .
?item wdt:P17 ?localisation .
?localisation wdt:P625 ?coordonnees .
?item schema:description ?itemdescription.
  FILTER(LANG(?itemdescription) = "fr")
?item wdt:P3815 ?observatoire

OPTIONAL {?item wdt:P2044 ?taille}
         {?item wdt:P18 ?pic}
    

SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en, fr" }
}
```

## Les différents types de volcan<a name="TypedeVolcan"></a>

Des éruptions significatives ont eu lieu 835 fois depuis l'an -455. Il existe 17 types de volcan différents 
parmis les volcans impliqués dans ces 835 éruptions. 

![TypeDeVolcan](https://user-images.githubusercontent.com/96179022/152225965-8c45462e-3df6-48ef-beec-1badd78ab8cf.jpg)

Nous voyons ici que les volcans les plus dangereux sont les stratovolcans (Volcan formé de couches stratifiées de laves ou de laves et de cendres selon le Larousse). 

## Répartition des volcans selon l'indice d'explosivité volcanique<a name="IEV"></a>

L’indice d’explosivité volcanique est une échelle utilisée pour comparer les éruptions volcaniques entre elles. Il a été mis au point en 1982 par Chris Newhall de l’USGS et Stephen Self de l’Université d’Hawaii.

![IEV](https://user-images.githubusercontent.com/96179022/152225856-0e013b54-d86d-41ea-98cb-f158794f9f63.jpg)

il est intéressant de voir que la majorité des éruptions ne possèdent pas un indice d'explosivité volcanique très élevé. Pour la plupart, l'indice d'explosivité est de 3. 
