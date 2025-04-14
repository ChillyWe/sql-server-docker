## 📁 Project Structure

```pgsql
docker/
├── sql-import/
│   └── your-database.bacpac
└── sql-package-image/
    └── Dockerfile
```
***
✅ 1. Ensure SQL Server is Running in Docker
Start it:
```bash
docker compose -f sql-server.yml up -d
```
✅ 2. Prepare .bacpac File

Place your .bacpac file into the docker/sql-import/ directory:

✅ 3. Build the Docker image with `sqlpackage`
```bash
cd docker/sql-package-image
docker build -t sqlpackage-image .
```
✅ 4. Run `sqlpackage` Container and Import .bacpac

Go to `sql-import` directory:
```bash
cd ../sql-import 
```
and then 
```bash
docker run --rm -it \                                                                                                                                                           INT ✘  6m 22s  
  -v "$(pwd)":/tmp \
  --network=host \
  sqlpackage-image bash
```
Inside the container, run:

```bash
sqlpackage /a:Import \
  /sf:/tmp/your-database.bacpac \
  /tsn:localhost \
  /tdn:ImportedDB \
  /tu:sa \
  /tp:'YourStrong!Passw0rd' \
  /ttsc:true

```

🧼 5. Exit and Verify

***# sql-server-docker
