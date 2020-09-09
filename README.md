# Harvester Deployment
This project is responsible for implementing the docker-compose stack of the Harvester application.

## Installation
Installing [docker](https://docs.docker.com/) and [docker-compose](https://docs.docker.com/compose/install/) is required to run the application.

Stack uses containers hosted on Whiteaster's docker registry. Images tagged "latest" are the latest stable versions.

Wherever there are placeholders, e.g. `grafana_api_key_here` or `PasswordHere123`, secure passwords should be generated or docker secret should be used.

### Application environment variables
The service `harvester_db` has the following variables:
```
- POSTGRES_USER=agregatorcmsusr
- POSTGRES_PASSWORD=PasswordHere123
- POSTGRES_DB=agregatorcms
```

The service `harvester_backend` has the following variables:
```
- DEBUG=False
- SECRET_KEY=secretdjangokey1234
- DB_ENGINE=django.db.backends.postgresql_psycopg2
- DB_NAME=harvester
- URL=${URL}
- DB_HOST=harvester_db
- DB_USER=harvesteruser
- DB_PASSWORD=PasswordHere123
- CELERY_BROKER_URL=redis://harvester_redis:6379/0
- DATAVERSE_URL=https://data-epuszcza.biaman.pl/
- DATAVERSE_API_KEY=dataverse_api_key_here
- LAYERS_PARENT_DATAVERSE=map
- MAPS_PARENT_DATAVERSE=map
- DOCUMENTS_PARENT_DATAVERSE=map
- DASHBOARDS_PARENT_DATAVERSE=meteo
- STUDIES_PARENT_DATAVERSE=dataibs
- GEONODE_URL=https://gis.openforestdata.pl/
- GRAFANA_URL=https://openforestdata.pl/grafana/
- GRAFANA_API_KEY=grafana_api_key_here
- ORTHANC_URL=https://ct.openforestdata.pl/
```

The service `harvester_flower` has the following variables:
```
- CELERY_BROKER_URL=redis://harvester_redis:6379/0
- FLOWER_PORT=8888
```

## Deployment
```
$ URL="localhost" docker-compose pull
$ URL="localhost" docker-compose up -d
```

The `URL` variables define the addresses on which the application is to be launched and on which frontend the backend listens.
The `URL` variable defines the target address of the application, for example `localhost` or `harvester.biaman.pl`.

In the configuration presented above, the application will be launched and will be available at `http://localhost`.

## Contribution
The project was performed by Whiteaster sp.z o.o., with register office in Chorzów, Poland - www.whiteaster.com and provided under the GNU GPL v.3 license to the Contracting Entity - Mammal Research Institute Polish Academy of Science in Białowieża, Poland.We are proud to release this project under an Open Source license. If you want to share your comments, impressions or simply contact us, please write to the following e-mail address: info@whiteaster.com