# Deploy A Machine Learning Model with FastAPI
This documents explains how to set up a machine learning project and deploy with FastAPI.

## Project setup
Before going through the steps make sure you have the following pre-installed

### Prerequisite
1. Python 3.6+
2. Virtualenv
3. Docker


Make sure to download/clone this repository and navigate to the folder in yout terminal. Now follow the indtructions below

1. Create the virtual environment.
```
    virtualenv /path/to/venv --python=/path/to/python3
```
You can find out the path to your `python3` interpreter with the command `which python3`.

2. Activate the environment and install dependencies.
    - #### Linux
    ```
        source /path/to/venv/bin/activate
        pip install -r requirements.txt
    ```

    - #### Windows
    ```
        ./path/to/venv/bin/activate
        pip install -r requirements.txt
    ```

3. Launch the service
```
    uvicorn api.main:app
```

## Posting requests locally
When the service is running, try this link in your browser
```
    127.0.0.1/docs
```

You can try the following curl command to see the model's response
```
    curl -X POST "http://localhost:8008/predict" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"data\":[[0.00632,18,2.31,0,0.538,6.575,65.2,4.09,1,296,15.3,396.9,4.98]]}"
```

## Deployment with Heroku
Check out this [article](https://testdriven.io/blog/fastapi-machine-learning/#heroku-deployment) to see how to deploy to heroku.

## Deployment with Docker
1. Build the Docker image
```
    docker build --file Dockerfile --tag mldemo .
```

2. Running the Docker image
```
    docker run -p 8000:8000 mldemo
```

3. Entering into the Docker image
```
    docker run -it --entrypoint /bin/bash mldemo
```

## docker-compose
1. Launching the service
```
    docker-compose up
```

This command looks for the `docker-compose.yaml` configuration file. If you want to use another configuration file,
it can be specified with the `-f` switch. For example  

2. Testing
```
    docker-compose -f docker-compose.test.yaml up --abort-on-container-exit --exit-code-from fastapi-ml-quickstart
```

# References
1. [How to properly ship and deploy your machine learning model](https://towardsdatascience.com/how-to-deploy-a-machine-learning-model-dc51200fe8cf). You can find repo [here](https://github.com/MaartenGr/ML-API)
2. [How to Deploy a Machine Learning Model](https://towardsdatascience.com/how-to-deploy-a-machine-learning-model-dc51200fe8cf). You can find repo [here](https://github.com/cosmic-cortex/fastAPI-ML-quickstart)
3. [Deploying and Hosting a Machine Learning Model with FastAPI and Heroku](https://testdriven.io/blog/fastapi-machine-learning/)
4. FastAPI docs: [Deployment](https://fastapi.tiangolo.com/deployment/), repository [here](https://github.com/tiangolo/uvicorn-gunicorn-fastapi-docker)
5. FastAPI doc: [Testing](https://fastapi.tiangolo.com/tutorial/testing/)
