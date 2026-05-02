**Homework 2: BERT on AWS**

BERT-based movie recommendation system using the MovieLens 1M dataset. Runs on an EC2 instance (t2.medium) inside a Docker container, with data and results stored on S3.

**How to Run**

1. SSH into EC2 with `ssh -i "your-key.pem" -L 8888:localhost:8888 ec2-user@<EC2_IP>`
2. Start Docker: `sudo systemctl start docker && sudo chmod 666 /var/run/docker.sock`
3. Run the container: `docker run -p 8888:8888 -v ~/homework_2:/home/jovyan/ my_jupyter`
4. Open `http://localhost:8888`, open `homework_2.ipynb`
5. Update AWS credentials in the credentials cell with fresh tokens from `mse-tl-dataeng300-EMR`
6. Run all cells top to bottom

**Functions**

- `download_movielens()` - downloads and extracts the MovieLens 1M zip
- `upload_dataset_to_s3()` - uploads dataset files to S3
- `download_dataset_from_s3()` - pulls dataset from S3 to local
- `dataset_exists_on_s3()` - checks if dataset already exists on S3
- `ensure_data_available()` - makes sure data is both local and on S3
- `load_movielens_data()` - loads movies, ratings, users into DataFrames
- `extract_year()` - pulls the release year from movie titles
- `build_movie_text()` - combines title, year, genres into a string for BERT
- `generate_embeddings()` - runs text through BERT and returns CLS embeddings
- `upload_file_to_s3()` - uploads a single file to S3
- `cosine_similarity()` - cosine similarity between user vector and movie embeddings
- `recommend_movies()` - returns top-N recommendations based on embedding similarity

**S3 Outputs (bucket: yegon-jay-hw2)**

- `ml-1m/` - raw dataset files
- `outputs/embeddings_pre1980.npy` - BERT embeddings for pre-1980 movies
- `outputs/movies_pre1980.csv` - pre-1980 movie metadata
- `outputs/recommendations_pre1980.json` - recommendations for top user and cold user (pre-1980)
- `outputs/embeddings_full.npy` - BERT embeddings for all movies
- `outputs/movies_full.csv` - full movie metadata
- `outputs/recommendations_full.json` - recommendations for top user and cold user (full data)
- `outputs/jay_profile.json` - my user profile with 10 rated movies
- `outputs/jay_recommendations.json` - 5 personalized recommendations for me

**AI Usage**

I used Claude AI for brainstorming pipeline structure, drafting helper functions, and debugging Docker/SSH issues. All code was reviewed and verified by me before running.
