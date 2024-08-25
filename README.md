# Movie Recommendation System

This repository contains a movie recommendation system built using cosine similarity. The system recommends movies based on the similarity of their tag descriptions. The recommendation engine utilizes a CountVectorizer to convert movie tags into a term-document matrix, which is then used to compute similarity scores between movies.

## Features

- **Movie Recommendations**: The system provides recommendations based on movie tags using cosine similarity.
- **Data Persistence**: Saved the movie dataset, movie dictionary, and similarity matrix using `pickle` for efficient loading and reuse.

## Files

- `movies.pkl`: Serialized movie dataset.
- `movie_dict.pkl`: Serialized movie dictionary for quick lookups.
- `similarity.pkl`: Serialized cosine similarity matrix.

## How It Works

1. **Data Preparation**: Tags are vectorized into numerical representations using `CountVectorizer`, with a maximum of 5000 features and English stop words removed.
2. **Similarity Computation**: The cosine similarity between the vectorized tag representations of movies is computed.
3. **Recommendation Function**: Given a movie title, the function identifies and prints the top 5 most similar movies based on their tag similarity.

## Usage

To use the recommendation system:

1. Load the pickled files:
    ```python
    import pickle
    new_df = pickle.load(open('movies.pkl', 'rb'))
    movie_dict = pickle.load(open('movie_dict.pkl', 'rb'))
    similarity = pickle.load(open('similarity.pkl', 'rb'))
    ```

2. Call the recommendation function with a movie title:
    ```python
    def recommend(movie):
        movie_index = new_df[new_df['title'] == movie].index[0]
        distances = similarity[movie_index]
        movie_list = sorted(list(enumerate(distances)), reverse=True, key=lambda x: x[1])[1:6]
        
        for i in movie_list:
            print(new_df.iloc[i[0]].title)
    
    recommend('Batman Begins')
    ```

## Example

For the movie "Batman Begins," the system might recommend:
- The Dark Knight
- Batman
- Batman
- 10th & Wolf
- The Dark Knight Rises

Feel free to explore and improve the system as needed!

---

Let me know if there's anything specific you'd like to adjust or add!
