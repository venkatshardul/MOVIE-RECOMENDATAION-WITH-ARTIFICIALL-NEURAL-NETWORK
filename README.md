Movie Recommendation System
This notebook demonstrates the development of a basic movie recommendation system using PyTorch. The system utilizes an Artificial Neural Network (ANN) with embedding layers to learn representations of users and movies, predicting ratings to suggest new movies to users.

Table of Contents
Project Objective
Dataset
Data Loading and Preprocessing
Model Architecture
Training and Evaluation
Making Recommendations
Project Objective
To build a movie recommendation system that can predict user ratings for unseen movies and provide personalized movie suggestions based on their historical preferences.

Dataset
The project uses a small version of the MovieLens dataset (ml-latest-small), which contains:

100,000 ratings
3,600 tag applications
9,000 movies
600 users
Data Loading and Preprocessing
Download and Extraction: The ml-latest-small.zip file is downloaded from GroupLens and extracted.
DataFrame Loading: movies.csv and ratings.csv are loaded into pandas DataFrames.
Feature Preparation: The timestamp column is dropped from the ratings_df.
Train-Test Split: The ratings_df is split into training and testing sets (80/20 ratio).
Tensor Conversion: userId and movieId are converted to 0-indexed PyTorch tensors, and ratings are converted to float32 tensors.
DataLoader Creation: TensorDataset and DataLoader are used to prepare the data for batch processing during training.
Model Architecture
The recommendation system uses an Artificial Neural Network (MovieRecommender) with the following structure:

Embedding Layers: Separate embedding layers for userId and movieId, each mapping to a 50-dimensional vector.
Concatenation: The user and movie embeddings are concatenated.
Dense Layers: A sequential model with three linear layers and ReLU activation functions:
Input layer: embedding_dim * 2 (100) neurons
Hidden layer 1: 128 neurons, ReLU activation
Hidden layer 2: 64 neurons, ReLU activation
Output layer: 1 neuron (for predicted rating)
Training and Evaluation
Optimizer: Adam optimizer with a learning rate of 0.001.
Loss Function: Mean Squared Error (MSELoss).
Epochs: The model is trained for 10 epochs.
Monitoring: Training and validation (test) loss are tracked per epoch.
Evaluation Metric: Root Mean Squared Error (RMSE) is used to evaluate the model's performance on the test set.
Making Recommendations
A recommend_movies function is provided to generate personalized movie recommendations for any given userId:

Identify Unrated Movies: It first determines which movies a user has not yet rated.
Predict Ratings: For these unrated movies, it uses the trained model to predict potential ratings.
Merge Information: Predicted ratings are merged with movie details (title, genres).
Sort and Recommend: The movies are then sorted by their predicted ratings in descending order, and the top N recommendations are returned.
