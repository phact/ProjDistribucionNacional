ProjDistribucionNacional
========================

##Proposito
Mapa de Colombia graphico en d3 por departamentos. Está hecho en js y html, no requiere app server ni compilación.

Features:
 - Coloreár basado en datos
 - Agregar puntos de interes (hoy son ciudades)
 - Actuar en mouseover

##Para empezar
instalar git y python version 2.x (u otro servidor web)

**descargar codigo**

git clone https://github.com/phact/ProjDistribucionNacional.git

**publicar hoja**

python -m SimpleHTTPServer

**abrir con browser**

http://localhost:8000/mapa.html

##Si hay que re-generar los datos:
ogr2ogr   -f GeoJSON   -where "ADM0_A3 IN ('COL')"   subunits.json   ne_10m_admin_0_map_subunits.shp

ogr2ogr   -f GeoJSON   -where "ISO_A2 = 'CO' AND SCALERANK < 10"   places.json ne_10m_populated_places.shp

topojson   -o col.json   --id-property SU_A3   --properties name=NAME   --   subunits.json   places.json

ogr2ogr   -f GeoJSON  -where "ADM0_A3='COL' and type='Departamento'" deptos.json ne_10m_admin_1_states_provinces.shp

topojson   -o col_deptos.json    --id-property SU_A3  --properties  --   subunits.json   places.json  deptos.json
