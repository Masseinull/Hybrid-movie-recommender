# Hybrid Movie Recommendation System

This project was completed for a Machine Learning course by a two-person group. It builds and evaluates a movie recommendation system using the **The Movies Dataset** (from IMDB).

The system explores and implements three distinct recommendation strategies: content-based filtering, user-user collaborative filtering, and a hybrid model that combines these approaches to provide more robust suggestions. The entire implementation is contained within the `ML_project.ipynb` Jupyter Notebook.

## Methodologies in Detail

1.  **Content-Based Filtering**: This model recommends movies by finding others with similar content and attributes.
    * **Feature Engineering**: It creates a "soup" of features for each movie by extracting and combining its metadata, including the director, top 3 cast members, genres, and keywords. The `ast.literal_eval` function is used to parse the stringified lists in the raw data.
    * **Vectorization**: The combined text-based features are converted into numerical vectors using `TfidfVectorizer`, which reflects the importance of a word to a movie in the collection of all movies.
    * **Similarity Calculation**: `cosine_similarity` is used to compute a similarity score between all pairs of movies based on their feature vectors. The `recommendation` function returns the most similar movies to a given title.

2.  **Collaborative Filtering (User-User)**: This approach recommends items based on the preferences of similar users, without needing to understand the item content.
    * **User-Item Matrix**: A matrix is constructed from the `ratings_small.csv` file, with users as rows, movies as columns, and ratings as the values.
    * **User Similarity**: Cosine similarity is calculated between users to find users with similar rating patterns.
    * **Recommendation**: The `recommend` function identifies users who liked a particular movie, finds other users most similar to them, and then suggests movies that this larger group of similar users rated highly.

3.  **Hybrid Model**: The `hybrid_recommendation_cbf` function implements a hybrid strategy. It starts with a movie title (an item-based approach) to identify an initial set of users who liked it. It then uses the collaborative filtering model to find a broader group of similar users and recommends movies from their collective preferences.

## Dataset
You can access the dataset zip file by this [link](https://drive.google.com/drive/folders/1fAMn3NRHXLaJ6XgJSbGEl-XYuDR9F3MO?usp=sharing)
## Installation Guide

Follow these steps to set up and run the project.

#### 1. Prerequisites
* Python 3.x
* pip package manager

#### 2. Clone the Repository
Clone this project to your local machine.
```bash
git clone https://github.com/Masseinull/Hybrid-movie-recommender.git
```

#### 3. Set Up a Virtual Environment (Recommended)
Navigate to the project directory and create a virtual environment.
```bash
# On macOS/Linux
python3 -m venv venv
source venv/bin/activate

# On Windows
python -m venv venv
.\venv\Scripts\activate
```

#### 4. Install Dependencies
Install the required packages using the `requirements.txt` file.
```bash
pip install -r requirements.txt
```

#### 5. Download the Dataset
This project uses **The Movies Dataset** from Kaggle. You will need to download it and place the following files in a location accessible by the notebook:
* `credits.csv`
* `keywords.csv`
* `links_small.csv`
* `movies_metadata.csv`
* `ratings_small.csv`

**Note**: The notebook is currently configured to load data from a Google Drive path. You will need to update the file paths in the notebook to match the location where you have stored the dataset.

## Usage

1.  Open the `ML_project.ipynb` notebook in a Jupyter environment.
2.  Update the file paths to the dataset CSVs.
3.  Run the cells sequentially to load data, preprocess features, and define the recommendation functions.

You can then call the primary functions to generate recommendations:

* `recommendation(movie_title, num_recommendations)`: Generates recommendations using the content-based model.
* `hybrid_recommendation_cbf(movie_title)`: Generates recommendations using the hybrid model.

**Example:**
```python
# Get 10 content-based recommendations for 'Pulp Fiction'
recommendation('Pulp Fiction', 10)
```

## Authors

This project was a collaborative effort by:
* A. Motevallian
* Mh. Arsalan
