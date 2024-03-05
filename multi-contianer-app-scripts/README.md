# Multi Container App - 2 Tier Web Application with Python Flask

🔥 **Acknowledgements:** These scripts use scripts from [CLO835-assignemnt1-Summer2023](https://github.com/ladunuthala/clo835_summer2023_assignment1)

---

### 📚 Step 1 - Installing the required MySQL package

```bash
sudo apt-get update -y
sudo apt-get install mysql-client -y
```

### 📚 Step 2 - Running application locally

```bash
pip3 install -r requirements.txt
sudo python3 app.py
```

Make sure you can run this `python flask` app locally and are comfortable making changes to it.

### 📚 Step 3 - Building Images locally

Building mysql docker image

```bash
docker build -t my_db -f Dockerfile_mysql
```

Building app docker image

```bash
docker build -t my_app -f Dockerfile
```

### 📚 Step 4 - Running mysql Container locally

Running mysql container

```bash
docker run -d -e MYSQL_ROOT_PASSWORD=pw  my_db
```

Get the IP of the database. You will need to later `export` it as `DBHOST` variable

```bash
docker inspect <container_id>
```

### 📚 Step 5 - Setting Runtime Variables

When DB is running as a local docker container and app will be running locally

```bash
export DBHOST=127.0.0.1
export DBPORT=3307
```

When DB is running a remote docker container and app will be running locally

```bash
export DBHOST=172.17.0.2
export DBPORT=3306
```

You need all the other run-time variables before building the app container

```bash
export DBUSER=root
export DATABASE=employees
export DBPWD=pw
export APP_COLOR=blue
```

### 📚 Step 4 - Running app Container locally

Running app container and passing runtime variables

```bash
docker run -p 8080:8080  \
    -e DBHOST=$DBHOST \
    -e DBPORT=$DBPORT \
    -e  DBUSER=$DBUSER \
    -e DBPWD=$DBPWD \
    -e DATABASE=$DATABASE \
    -e APP_COLOR=$APP_COLOR \
    my_app
```

At this stage, you must make sure the website is accessible in the browser
