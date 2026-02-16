
airflow-project/
│
├── dags/
├── data/
│   ├── raw.csv
│   └── processed.csv



# Step 1:
change to the project directory 

# Step 2 :Create Virtual Environment
python -m venv .venv
source .venv/bin/activate   # Mac/Linux
.venv\Scripts\activate      # Windows

# Step 3
Once the .venv is activated then only run this 

export PATH="$(pwd)/.venv/bin:$PATH"

which python

# Step 4
Upgrade pip:

pip install --upgrade pip

# Step 5
# Install Apache Airflow (Local Dev Version)

Airflow requires a specific constraints file.

✅ Recommended install (Airflow 2.8+ example)

AIRFLOW_VERSION=2.8.4
PYTHON_VERSION=3.10
CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"


⚠️ Make sure your Python version matches the constraints file.

# Step 6
# ⚙️  Set  Airflow Home directory


export AIRFLOW_HOME=$(pwd)/airflow_home

Windows:
set AIRFLOW_HOME=%cd%\airflow_home



# Step 7
# initialize database:

airflow db init

Create admin user:

airflow users create \
  --username admin \
  --firstname Admin \
  --lastname User \
  --role Admin \
  --email admin@example.com \
  --password admin


# Step 8
# Install PySpar
pip install pyspark

# Step 9
# Create Spark ETL Script

Create file:

etl_spark.py

Test manually:

python etl_spark.py


# Step 10

Orchestrate with Airflow

Create DAG:

dags/spark_etl_dag.py


# Step 11
# Start Airflow Locally

👉 If you want to start in a new  terminal ,it must have the .venv activated.

In  a new Terminal 2:
cd airflow/airflow-local-etl
source .venv/bin/activate 
export AIRFLOW_HOME=$(pwd)/airflow_home

which python
 which airflow

# Now Run ETL

Start Airflow:

airflow standalone


Go to UI
Enable spark_etl_pipeline
Trigger it

Check:

data/processed.csv


You should see:

Only Alice & Charlie

Salary increased by 10%


Now open:

http://localhost:8080


Login:

Username: admin

Password: admin

🎉 Airflow is running locally!


Note: kill if previous one is running
kill -9 9714




# Trigger
airflow dags trigger spark_etl_pipeline

airflow tasks test spark_etl_pipeline run_spark_etl 2024-01-01
