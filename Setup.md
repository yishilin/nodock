
# How to setup nodejs + nginx

1. Prepare your nodejs app directory

    Says it is `~/apps/my_awsome_app/`

    Regarding the content of ,pls refer to https://github.com/yishilin/nodock/tree/master/_examples/nginx,
    you could copy from: <br>
    `cp nodock/_examples/nginx/* ./my_awesome_app/`

    Note:
    * Your directory need include index.js as the container will use `nodemon index.js` to start
    * container will npm install the pagckages in `package.json`

2. Clone nodock repo
    ```
    cd SOME_WORKING_DIRECTORY
    git clone https://github.com/yishilin/nodock.git
    ```


3. Setup app directory in docker container
    ```bash
    cd SOME_WORKING_DIRECTORY/nodock/
    vim docker-compose.yml

    node:
        volumes:
          - ~/apps/my_awsome_app/:/opt/app
    ```

    Note: <br>
    This going to map local `~/apps/my_awesome_app/` directory to contianer `/opt/app` directory


4. Build the images
    ```bash
    cd SOME_WORKING_DIRECTORY/nodock/
    sudo docker-compose build
    ```


5. Run the containers
    ```bash
    cd nodock
    sudo docker-compose up -d node nginx
    sudo docker-compose ps

    curl http://0.0.0.0
    ```


6. Start development
   Use your IDE/Editor like vscode to work on local directory `~/apps/my_awesome_app`, it will run in the nodejs container.


7. Some commands:
    ```bash
    sudo docker-compose ps
    sudo docker-compose stop
    sudo docker-compose pause
    sudo docker-compose start
    sudo docker-compose restart
    sudo docker-compose up -d node nginx
    sudo docker-compose down

    #login the container ssh:
    docker exec -it CONTAINER_NAME sh
    docker exec -it CONTAINER_ID bash
    docker exec -it CONTAINER_ID ip addr
    ```

    kill: just kill container process without cleanup, no mem used anymore
    stop/start: kill container process and will cleanup, no mem
    pause/unpause: not kill the container process but suspend the process, still consume mem