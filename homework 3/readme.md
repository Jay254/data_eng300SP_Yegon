**Homework 3: NYC Taxi Analytics with PySpark on EC2**

**How to run**

1. Launch an EC2 instance in `us-east-1` (Amazon Linux, 80 GiB storage).

2. SSH in with port forwarding:

    - ssh -i "jayjay254.pem" -L 8888:localhost:8888 ec2-user@<EC2_PUBLIC_DNS>

3. Install dependencies:

    - sudo dnf install -y java-17-amazon-corretto-devel python3 python3-pip
    - python3 -m venv ~/pyspark-venv
    - source ~/pyspark-venv/bin/activate
    - pip install pyspark jupyter pandas pyarrow matplotlib awscli

4. Configure AWS credentials:

    - aws configure

5. Copy data from the class S3 bucket:

    - mkdir -p ~/taxi_data
    - aws s3 cp "s3://de300-hw3-nyctlc-549787090008-us-east-1-an/yellow_tripdata_2026-01.parquet" ~/taxi_data/
    - aws s3 cp "s3://de300-hw3-nyctlc-549787090008-us-east-1-an/green_tripdata_2026-01.parquet" ~/taxi_data/

6. Start Jupyter:

    - source ~/pyspark-venv/bin/activate
    - jupyter notebook --no-browser --port=8888

7. Open `http://localhost:8888` in your browser, open `hw3_nyc_taxi.ipynb`, and run all cells.

**S3 output paths**

Results are written to `s3://yegon-de300-hw3/nyc-taxi-assignment/`:
- `trips_by_type.csv`
- `avg_fare_by_type.csv`
- `pickups_by_hour.csv`
- `fare_prediction_plot.png`
