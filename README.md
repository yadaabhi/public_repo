# EnsoMate XRAY Backend

### Set up the oracle-db container

```
docker pull container-registry.oracle.com/database/free:latest-lite

docker run --name oracle-db -p 1521:1521 -v ./data:/opt/oracle/oradata -e ORACLE_PWD={password} -d container-registry.oracle.com/database/free:latest-lite
```

### Install libmagic

```
brew install libmagic // will be different on Windows
```

### Python environment set-up

```
python -m venv .venv
source .venv/bin/activate (for windows: source .venv/Scripts/activate)
pip install -r requirements.txt

> **Note for Windows users:**  
> `uvloop` is not supported on Windows.  
> Before running the command below, open `requirements.txt` and remove or comment out the `uvloop` line.
```

### Running the code

1. Set up .env file
2. Run alembic migrations, run the below command after activating venv.
```
alembic upgrade head
```
3. Run the application.
```
uvicorn app.main:app --reload
```

4. docker pull rabbitmq:management-alpine
   docker run -p 5672:5672 -p 15672:15672 -d rabbitmq:management-alpine

5. python -m workers.grype_worker
   python -m workers.outbox_poller
   and all other workers

6. choco install syft -y (or equivalent in mac)

7. choco install grype -y (or equivalent in mac)

8. create a user
   get access token
   create a product
   create scanners using the API with scan types:
    sbom_gen
    vuln_scan
   upload an artifact 