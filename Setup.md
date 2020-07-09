
# How to setup nodejs + nginx

1. Prepare your nodejs app directory
   Says it is ~/apps/my_awsome_app/
    cp nodock/_examples/nginx/* ./node_app

2. clone nodock
cd SOME_WORKING_DIRECTORY
git clone https://github.com/yishilin/nodock.git

3. setup directory in docker container
cd SOME_WORKING_DIRECTORY/nodock/
vim docker-compose.yml

node:
    volumes:
      - ~/apps/my_awsome_app/:/opt/app

Note: pls remember to map local ~/apps/my_awesome_app/ directory to contianer /opt/app directory


4. Build the images
cd SOME_WORKING_DIRECTORY/nodock/
sudo docker-compose build


5. Run the containers
cd nodock
sudo docker-compose up -d node nginx
sudo docker-compose ps

curl http://0.0.0.0

