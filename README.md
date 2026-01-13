
# Database Migration - Backend

Backend for migrating a MySQL project from a local database to a cloud (Azure) platform.
## how it works
create _history_table to store updates in the old db  
create triggers for INSERT, UPDATE, DELETE and use (old_primary_keys, version_number) as composite primary key   
update the tables according to the latest version for each row that was updated according to the history table  


for updates use INSERT ... ON DUPLICATE KEY UPDATE
for delete just use delete by primary key

check the table_names, check the total row numbers, check random percentage of rows data (ORDER BY RAND()), check all rows data
## Set up

### Set up virtual environment
Navigate to project root directory, then set up virtual environment:
#### OSX/Linux
```bash
python3 -m venv .venv

```
#### Windows
```cmd
py -3 -m venv .venv
```

### Activate the environment

#### OSX/Linux
```bash
. .venv/bin/activate
```

#### Windows
```cmd
.venv\Scripts\activate
```
### Install dependencies

```bash
pip install flask
pip install sqlalchemy
pip install pymysql
pip install mysql-connector-python

# if testing
pip install python-dotenv
```

### Create environment file (only required for testing)
Create a file called `.env` in the root directory. It should contain the following data:
```json
MY_LOCAL_DB_URL=your_local_db_url
MY_LOCAL_DB_USERNAME=your_local_db_username
MY_LOCAL_DB_PASSWORD=your_local_db_password
MY_CLOUD_DB_URL=your_cloud_db_url
MY_CLOUD_DB_USERNAME=your_cloud_db_username
MY_CLOUD_DB_PASSWORD=your_cloud_db_password
```

## Run Server Locally

Start the server using the following command:
```bash
flask --app main run --debug
```
Make requests to `localhost:5000`

the `--debug` flag means the server will auto-reload when a change is detected.

## Testing
Run tests using the following command:
```bash
python .\tests\{test_filename.py}
```
The test file will automatically start and terminate the server.
