#linux #infra
O IP externo/público pode ser obtido em vários sites como o site abaixo: 

[Ver Dirección de Geo IP - Ver información de dirección de GEO IP y localizar el IP en un mapa](https://es.geoipview.com/)

ou

[Ver Dirección de Geo IP - Ver información de dirección de GEO IP y localizar el IP en un mapa](https://es.geoipview.com/)

Podemos também obter o IP através do comando a seguir:

```bash
host myip.opendns.com resolver1.opendns.com | grep "myip.opendns.com has" | awk '{print $4}'
```