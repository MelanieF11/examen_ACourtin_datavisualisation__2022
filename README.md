# Les volcans et tsunamis depuis toujours

### Titre 2

> Répertoire servant pour l'examen final d'Antoine Courtin, datavisualisation

Faire une liste
* 1
* 2
* 3




## Présentation des volcans



Voici la galerie d'image permettant de voir tous les volcans répertoriés sur Wikidata:

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
