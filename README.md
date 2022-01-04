# ArrangoDb-Movie-Catalog
Kevin Bacon 6 Degree of Separation

# ArrangoDb docker setup - 
https://www.youtube.com/watch?v=eDsK3ZhwNrQ

docker run -e ARANGO_RANDOM_ROOT_PASSWORD=1 -d --name arangodb-instance arangodb

To launch arragosh from docker cliet , click CLI from container and click command to connect with root.

arangosh

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
/ # arangosh
Please specify a password:

                                       _
__ _ _ __ __ _ _ __   __ _  ___  ___| |__
/ _` | '__/ _` | '_ \ / _` |/ _ \/ __| '_ \
| (_| | | | (_| | | | | (_| | (_) \__ \ | | |
\__,_|_|  \__,_|_| |_|\__, |\___/|___/_| |_|
|___/

arangosh (ArangoDB 3.8.4 [linux] 64bit, using jemalloc, build tags/v3.8.4-0-gefd5a33bb1a, VPack 0.1.35, RocksDB 6.8.0, ICU 64.2, V8 7.9.317, OpenSSL 1.1.1l  24 Aug 2021)
Copyright (c) ArangoDB GmbH

Command-line history will be persisted when the shell is exited. You can use `--console.history false` to turn this off
Connected to ArangoDB 'http+tcp://127.0.0.1:8529, version: 3.8.4 [SINGLE, server], database: '_system', username: 'root'

Type 'tutorial' for a tutorial or 'help' to see common examples
127.0.0.1:8529@_system>
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Import CSV available in movie-catalog directory.

Importing/exporting CSV from local machine

From LocalMachine To DockerContainer
$docker cp C:/localMachineSourceFolder/someFile.txt containerId:/containerDestinationFolder

From DockerContainer To LocalMachine
$docker cp containerId:/sourceFilePath/someFile.txt C:/localMachineDestinationFolder

Importing File into DB from arrangosh

from arrangosh to arrangoDB import command

# Sample command
arangoimport --file '/home/airports.csv' --collection airports --create-collection true --type csv


# Running Queries on UI 
Launch graph UI and run below query

for e in 1..6 ANY K_SHORTEST_PATHS 'name_basics/nm0000102' TO 'name_basics/nm0000158'
Graph 'movie_catalog'
limit 10
return {degree:e.weight-1,name:e.vertices[*].name}


# Sample Data
https://www.arangodb.com/docs/stable/aql/examples-actors-and-movies.html

to get docker id run command  docker ps
91955@rajnish MINGW64 ~
$ docker ps
CONTAINER ID   IMAGE                     COMMAND                  CREATED        STATUS             PORTS                    NAMES
83e7e87d422e   arangodb/arangodb:3.8.4   "/entrypoint.sh aran…"   16 hours ago   Up About an hour   0.0.0.0:8529->8529/tcp   focused_montalcini

C:\Users\91955\Downloads\arrangodb\GraphCourse_DemoData_ArangoDB-2\airports.csv
C:\Users\91955\Downloads\arrangodb\GraphCourse_DemoData_ArangoDB-2\flights.csv


From LocalMachine To DockerContainer
docker cp "C:\Users\91955\Downloads\arrangodb\GraphCourse_DemoData_ArangoDB-2\airports.csv" 83e7e87d422e:/home/
docker cp "C:\Users\91955\Downloads\arrangodb\GraphCourse_DemoData_ArangoDB-2\flights.csv" 83e7e87d422e:/home/

from arrangosh to arrango DB import command

command --> arangoimport --file '/home/airports.csv' --collection airports --create-collection true --type csv
console Output.
/ # arangoimport --file '/home/airports.csv' --collection airports --create-collection true --type csv
Please specify a password:
Connected to ArangoDB 'http+tcp://127.0.0.1:8529, version: 3.8.4, database: '_system', username: 'root'
----------------------------------------
database:               _system
collection:             airports
create:                 yes
create database:        no
source filename:        /home/airports.csv
file type:              csv
quote:                  "
separator:
headers file:
threads:                2
on duplicate:           error
connect timeout:        5
request timeout:        1200
----------------------------------------
Starting CSV import...
2021-12-31T04:19:40Z [227] INFO [9ddf3] {general} processed 262144 bytes (3%) of input file

created:          3375
warnings/errors:  0
updated/replaced: 0
ignored:          0
lines read:       3377
/ #
------------------------------


	
	
