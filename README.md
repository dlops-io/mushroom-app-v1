# Mushroom App - Setup & Code Organization

In this tutorial we will setup two containers:
* api-service
* frontend-simple

The following container architecture is what we will implement:
<img src="images/container-architecture.png"  width="800">

## Prerequisites
* Have Docker installed
* Have VSCode or editor of choice


## Setup Environments
In this tutorial we will setup containers to run python code for creating APIs and a container to run HTML web server.

### Clone the github repository
- Clone or download from [here](https://github.com/dlops-io/mushroom-app-v1)

### Create a local **secrets** folder

It is important to note that we do not want any secure information in Git. So we will manage these files outside of the git folder. At the same level as the `mushroom-app-v1` folder create a folder called **secrets**

Your folder structure should look like this:
```
   |-mushroom-app-v1
     |-images
     |-src
       |---api-service
       |---frontend-simple
   |-secrets
```

## Frontend App (Simple) Container
We will build a simple frontend app that uses basic HTML & Javascript. 

### Go into the frontend-simple folder 
- Open a terminal and go to the location where `mushroom-app-v1/frontend-simple`

### Build & Run Container
- Run `sh docker-shell.sh` or `docker-shell.bat` for windows


### Start Web Server
- To run development web server run `http-server` from the docker shell
- Test the web app by going to `http://localhost:8080/`

### Edit Code in VS Code
- Open `index.html` in your editor
- Add some text using the `<p>` tag in the html
```
<body>
    🍄 Welcome to the mushroom identification App!
    <p>
        This is a placeholder for the awesome mushroom identification app
    </p>
</body>
```
- Refresh the page `http://localhost:8080/`
- You will see your changes in the web page


## Backend API Container
We will create a basic backend container to run our REST API. The FastAPI framework will be used for this.

### Go into the api-service folder 
- Open a terminal and go to the location where `mushroom-app-v1/api-service`

### Build & Run Container
- Run `sh docker-shell.sh` or `docker-shell.bat` for windows


### Start API Service
- To run development API service run `uvicorn api.service:app --host 0.0.0.0 --port 9000` from the docker shell
- Test the API service by going to `http://localhost:9000/`

### Edit Code in VS Code
- Open `api/service.py` in your editor
- Add the following code at the end of the file:
```
@app.get("/square_root/")
async def square_root(x: float = 1, y: float = 2):
    z = x**2 + y**2
    return z**0.5
```
- Go to `http://localhost:9000/square_root/`
- Do you see the square root computed by a python function displayed in the web browser?
- Go to `http://localhost:9000/square_root/?x=2&y=10` adding parameters to your url
- Do you see the new results?

---

## Docker Cleanup

### Make sure we do not have any running containers and clear up an unused images
* Run `docker container ls`
* Stop any container that is running
* Run `docker system prune`
* Run `docker image ls`