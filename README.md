# kgwebmap: Knowledge Graph Web Map
A very simple MapLibre web map to display and manually query a knowledge graph containing GeoSPARQL geometries.

 ![kgwebmap example](kgwebmap.png)

## SPARQL knowledge graph
The web map retrieves data from an knowledge graph accessible via a SPARQL endpoint. 

[Apache Jaena Fuseki](https://jena.apache.org/documentation/fuseki2/) is recommended as an easy-to-use triple store (graph database) and SPARQL endpoint. Instructions for [installing Fuseki and creating a knowledge graph](https://medium.com/@rrichajalota234/how-to-apache-jena-fuseki-3-x-x-1304dd810f09) are widely available. OSX users can install in minutes through a package manager like Homebrew, for example. 

An example knowledge graph containing the gazetted placenames for Australia, structured using the FSDF Placename ontology can be downloaded from the [RMIT Geographic Knowledge Lab](http://gkl.rmit.melbourne) below:

- [Placenames Australia knowledge graph](http://gkl.rmit.melbourne/kg/pnkg_2025_03_18.ttl)

You can verify your SPARQL endpoint is working correctly by running a simple SPARQL query on the created knowledge graph, such as below. 

```
PREFIX pn: <http://linked.data.gov.au/def/placenames/>
PREFIX geo: <http://www.opengis.net/ont/geosparql#> 
SELECT  ?loc ?geom ?name ?category
WHERE   {
        ?loc geo:asWKT ?geom .
        ?place geo:hasGeometry ?loc .
        ?place pn:hasPlaceClassification ?category .
        ?place pn:hasPlaceName ?plnm .
        ?plnm pn:name ?name
}
LIMIT 100
```

## Maplibre web map

The kgwebmap is based on an updated version of the EPFL DHLAB [leaflet-sparql](https://github.com/dhlab-epfl/leaflet-sparql) repo converted to MapLibre. 

- [kgwebmap html file](kgwebmap.html)

