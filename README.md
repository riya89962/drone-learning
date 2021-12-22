# drone-learning

## Contents

* [Drone CI - Hello World](#getting-started-with-drone-ci---hello-world-example)
* [References](#references)

## Getting started with drone ci - Hello world example

Set up a drone server with github

### What we need?

1. Docker
2. Publically accessible domain name for drone server
3. Source code management provider (SCM)
4. SCM - OAuth application
5. Drone server
6. Drone runner: to execute build pipelines.
7. SCM - repository

### Implementation

1. Install docker.
2. Start docker.
3. ngrok can be used to provide publically accessible domain name to drone server.
    1. Sign Up
    2. Install ngrok &rarr; unzip &rarr; add ngrok to path.
    3. Configure ngrok with your auth token.
    `./ngrok authtoken REPLACE_WITH_YOUR_AUTHTOKEN`
    4. Expose the port (at which drone server would be running on host machine) to the internet.

    ```bash
    ./ngrok REPLACE_WITH_SERVICE_PROTOCOL REPLACE_WITH_DRONE_SERVER_PORT

    # Drone service protocol: http or https
    ```

4. Github can be chosen for SCM.
5. [Create OAuth application with Github](https://docs.drone.io/server/provider/github/#create-an-oauth-application). Note the Github client id and client secret.
6. Create Github repository. Add the [drone configuration file](/hello-world/.drone.yml) (conventionally .drone.yml) to this repository.
7. Start drone server and drone runner (Docker runner can be chosen for drone runner.)
    1. Create [docker-compose.yml](/hello-world/docker-compose.yml) locally
    2. Create .env file (in same directory as docker-compose.yml) & add following variables

        ```env
        DRONE_GITHUB_CLIENT_ID=REPLACE_WITH_DRONE_GITHUB_CLIENT_ID
        DRONE_GITHUB_CLIENT_SECRET=REPLACE_WITH_DRONE_GITHUB_CLIENT_SECRET
        DRONE_RPC_SECRET=REPLACE_WITH_DRONE_RPC_SECRET

        DRONE_SERVER_HOST=REPLACE_WITH_DRONE_SERVER_HOST
        DRONE_SERVER_PROTO=REPLACE_WITH_DRONE_SERVER_PROTO

        DRONE_RPC_HOST=REPLACE_WITH_DRONE_RPC_HOST
        DRONE_RPC_PROTO=REPLACE_WITH_DRONE_RPC_PROTO

        DRONE_RUNNER_CAPACITY=REPLACE_WITH_DRONE_RUNNER_CAPACITY
        DRONE_RUNNER_NAME=REPLACE_WITH_DRONE_RUNNER_NAME
        ```

    3. Run `docker-compose up`.

8. From browser, go to drone server host url. Sign up.
9. Select the target github repository and activate repository.
10. Make some changes in the repository and commit.
11. In the drone server UI, we can see the build job gets triggered.

## References

* [Drone CI installation guide - Github](https://docs.drone.io/server/provider/github/)
* [ngrok](https://ngrok.com/)
* [Ngrok Step by Step Guide](https://www.sitepoint.com/use-ngrok-test-local-site/)
* [Create Oauth application](https://docs.drone.io/server/provider/github/#create-an-oauth-application)
