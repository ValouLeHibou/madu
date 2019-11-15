# MADU

![Python](https://img.shields.io/badge/Python-3.6-yellow)
![Flask](https://img.shields.io/badge/Flask-1.1.1-lightgrey)
![Docker](https://img.shields.io/badge/Docker-19.03-blue)
![Postgres](https://img.shields.io/badge/Postgres-11.0-purple)
![Postgis](https://img.shields.io/badge/Postgis-2.5-green)
![Qis](https://img.shields.io/badge/Qgis-3.1-gree)

**Ce projet a été réalisé dans le cadre du hackathon de l'ECV digital**

<!-- language: lang-none -->
      ______ _______      __  _____  _       _ _        _ 
     |  ____/ ____\ \    / / |  __ \(_)     (_) |      | |
     | |__ | |     \ \  / /  | |  | |_  __ _ _| |_ __ _| |
     |  __|| |      \ \/ /   | |  | | |/ _` | | __/ _` | |
     | |___| |____   \  /    | |__| | | (_| | | || (_| | |
     |______\_____|   \/     |_____/|_|\__, |_|\__\__,_|_|
                                        __/ |             
                                       |___/          

Groupe 6 :

- GUILBAUD Valentin_____M1 DEV
- VENCO Antoine_________M2 WD
- KHUNJA Myriam_________M2 WM
- PÂQUET Bérénice_______M1 UX
- BERGERON Steven_______M2 UX


## Choix des technos

Soyons honnêtes, étant le seul développeur dans mon groupe, je ne me suis pas privé de quelques fantasies.
J'ai donc décidé de travailler soit sur des technologies que je "maitrise" et que je souhaite approfondir :
- Python
- Flask
- Docker

Soit sur des technologies sur lesquels je n'ai pas encore eu la chance de travailler (ou tout du moins pas en profondeur) :
- SQLAlchemy
- Postgres
- Postgis
- pgadmin
- Qgis 


En termes plus technique, mon choix est tout de même réfléchi :
- Python s'oriente vers le traitement du big data, vi à vi de la cartographie de lieux dans le monde, ce choix me semblait pertinent.

- N'ayant que peu de temps et souhaitant réalisé un CRUD afin de pouvoir insérer facilement de nouvelles coordonnées dans une BDD, Flask se trouve être le framework parfait. Simple et très léger, grace à lui je vais pouvoir réaliser beaucoup de features plus ou moins complexe en peu de temps.

- En ce qui concerne Docker, ce n'est rien de plus qu'un caprice de ma part. Docker n'est pas viable en ce qui concerne les petis projets, en revanche si l'application venait à grossir, la question d'utiliser Docker pourrai bien se poser.

- Après quelques renseignement, prosgresql se trouve être la BDD parfaite pour le traitement de nombreuses coordonnées sur une carte. Le souci de la rapidité étant un des points les plus importants soulevé par l'intervenante, le choix fut rapidement fait.

- L'utilisation de Postgis et de Qgis s'insèrent dans la même logique. Qgis fesant écho à postgis, il n'était pas concevable de passer à coté.

-------
**Ayant réalisé un gros travail d'infrastructure et ne pouvant le rendre comme un code à push sur git, ce README sera généreusement garni de screenshoot accompagnés d'explications décrivant mes démarches.**

## Développement Docker/Flask/Postgresql pour le CRUD

Dans le cadre du projet, j'ai tout d'abord mis en place un conteneur docker `Postgresql` via dockerhub :
https://hub.docker.com/_/postgres

```
docker run -it --rm --network some-network postgres psql -h some-postgres -U postgre
```


Par la suite, j'ai modifier l'image pour finalement utilisé une image `postgis` couplé à une image `pgadmin` en concordance avec Qgis que j'utiliserai plus tard :
https://hub.docker.com/r/mdillon/postgis

J'ai ensuite réalisé un fichier  `docker-compose.yaml` afin de pouvoir résalisé un montage rapide des conteneurs postgis et pgadmin

Voulant réalisé un CRUD dans le but d'insérer de nouveaux points de géolocalisation dans la base de donnée, j'ai réalisé une connexion basique à mon conteneur `postgis` disponible de le fichier `app.py`.

Malheureusement ce point ne se sera jamais confirmé. A cause d'un bug de configuration de l'image `postgis` dans le package `psycopg2` et selon certains forum, il m'aurai falu réinstaller toute ma configuration postgresql.


## Qgis  

Pour palier à ce manque, l'outil `Qgis` à fait son apparation.
