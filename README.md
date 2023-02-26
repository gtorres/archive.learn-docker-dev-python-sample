## Create virtual environment

python3 -m venv .venv
source .venv/bin/activate

(.venv) $ python3 -m pip install Flask
(.venv) $ python3 -m pip freeze > requirements.txt

### Use source .venv/bin/activate
Whenever working in this project

## Run the application
This isn't really necessary once the process is figured out
(.venv) $ python3 -m flask run

## Run mysql container

docker run --rm -d -v mysql:/var/lib/mysql \
	-v mysql_config:/etc/mysql -p 3306:3306 \
	--network mysqlnet \
	--name mysqldb \
	-e MYSQL_ROOT_PASSWORD=p@ssw0rd1 \
	mysql

The above command requires 2 volumes and a network.

docker volume create mysql
docker volume create mysql_config
docker network create mysqlnet

## Check that mysql works

docker exec -ti mysqldb mysql -u root -p

## Build the web container

docker build -t python-docker .

## Run it using the network

docker run --rm -d --network mysqlnet \
	--name rest-server \
	-p 8000:5000
	python-docker

You should be able to call the routes and get a response using

https://localhost:8000/initdb
https://localhost:8000/widgets
