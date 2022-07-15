# Cartopartie à Claix

Fichiers et cartes utiles à l'organisation d'une [cartopartie à Claix](https://wiki.openstreetmap.org/wiki/Cartopartie_Claix_du_10-09-2022) (Isère) le 10 septembre 2022 par le [groupe local](https://wiki.openstreetmap.org/wiki/Grenoble_groupe_local) des contributeurs à OpenStreetMap de Grenoble.


# Fichiers

## Limites communales

- claix-limit.png : carte 
- claix-limit.geojson : limites (pour utilisation sur le Tasking Manager)
- claix-limits-api.txt : requête Overpass

# Répertoires

## cadastre

Fichiers téléchargés depuis http://cadastre.openstreetmap.fr/  

## maps

Cartes de la commune à différents niveaux de zoom générées en utilisant [go-staticmaps](https://github.com/flopp/go-staticmaps)

script :  claix-maps.cmd

### Procédure de génération de la carte

- Logiciels nécessaires
    - [osmtile](https://github.com/JVillafruela/osmtile/releases) (shameless plug 😉​)
    - [go staticmaps](https://github.com/flopp/go-staticmaps)
- [obtenir](http://overpass-turbo.eu/?Q=%2F%2F%20Ville%20de%20Claix%20(Is%C3%A8re%20par%20le%20code%20INSEE)%0Aarea%5B%22ref%3AINSEE%22%20%3D%20%2238111%22%5D-%3E.city%3B%0Arel(pivot.city)%3B%0Away(r)%3B%20%2F%2F%20ways%20de%20la%20relation%0A%2F%2Fway(r%3A%22outer%22)%3B%0Aout%20body%3B%0A%3E%3B%0Aout%20skel%20qt%3B&C=45.1186;5.67135;13) les limites communales et les exporter en geojson
- aller sur http://bboxfinder.com et cliquer sur "enter coordinates". Coller le contenu du fichier geojson et cliquer sur "add" 
- copier la ligne "Box" (5.618289,45.088666,5.700169,45.148789). Notez l'ordre : longitude,latitude.
- calculer la taille de carte :
```bash
osmtile --lon-lat --zoom 15 5.618289,45.088666,5.700169,45.148789
X: 16895..16902 (8) Y: 11776..11768 (9)
Map size : width=2048 height=2304
```
- générer la carte : 
```bash
create-static-map --type=osm --bbox="45.088666,5.618289|45.148789,5.700169" --zoom=15 --output=claix-15.png --width=2048 --height=2304 
```


## tiles

Cache des tuiles go-staticmaps (Z/X/Y).
Sous Windows le cache se trouve dans C:\Users\%USERNAME%\AppData\Local\flopp.net\go-staticmaps\Cache\0.1