Overview

This project implements a movie recommender system using Singular Value Decomposition (SVD) from the surprise library.
The system predicts movie ratings for users based on historical data and generates personalized movie recommendations.



How It Works

1.Load the data

movies_df = pd.read_csv('movies.csv')
ratings_df = pd.read_csv('ratings.csv')
df = pd.merge(ratings_df, movies_df[['movieId', 'genres']], on='movieId', how='left')


2.Encode IDs and genres

df['userId'] = LabelEncoder().fit_transform(df['userId'])
df['movieId'] = LabelEncoder().fit_transform(df['movieId'])
df = df.join(pd.DataFrame(MultiLabelBinarizer().fit_transform(df.pop('genres').str.split('|')),
                          columns=mlb.classes_, index=df.index))


3.Train/Test split

train_df, test_df = train_test_split(df, test_size=0.2)


4.Build and train the SVD model

reader = Reader(rating_scale=(0.5, 5))
data = Dataset.load_from_df(train_df[['userId', 'movieId', 'rating']], reader)
trainset = data.build_full_trainset()
model_svd = SVD()
model_svd.fit(trainset)


5.Evaluate model

predictions = model_svd.test(trainset.build_anti_testset())
accuracy.rmse(predictions)


6.Generate top-N recommendations

def get_top_n_recommendations(user_id, n=5):
    user_movies = df[df['userId'] == user_id]['movieId'].unique()
    all_movies = df['movieId'].unique()
    movies_to_predict = list(set(all_movies) - set(user_movies))
    predictions = model_svd.test([(user_id, mid, 0) for mid in movies_to_predict])
    top_n = sorted(predictions, key=lambda x: x.est)[:n]
    top_ids = [int(pred.iid) for pred in top_n]
    return movie_encoder.inverse_transform(top_ids)


Usage

Place your movies.csv and ratings.csv in the project directory.

Run the recommender script:

python recommender.py


Enter a userId when prompted.

View the top 5 recommended movies for that user.

Example Output
What userid would you like recommendations for? 123
Top 5 Recommendations for User 123:
1. Speed 2: Cruise Control (1997)
2. Batman & Robin (1997)
3. Godzilla (1998)
4. Wild Wild West (1999)
5. Battlefield Earth (2000)

