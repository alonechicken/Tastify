# Tastify
Data Project using spotify music data to create a music recommender

###
A command-line tool to discover new music based on your specific taste. This content-based recommendation system takes your desired audio features (like danceability, energy, and mood) and a chosen genre to recommend songs from a vast dataset of Spotify tracks.


## 1.0 Project Goal

The goal of this project is to solve this problem by providing a tool that allows users to act as their own music curators. By inputting specific audio feature preferences, users can get highly personalized song recommendations, turning a massive library of music into a tailored discovery experience.

## 2.0 Data Source
The dataset used for this project is the "Spotify Tracks DB" sourced from Kaggle. It contains audio feature information for over 170,000 songs, providing a rich and diverse foundation for building the recommendation engine and clustering models.

## 3.0 Project Assumptions

1. A user's musical taste and mood can be reasonably quantified by Spotify's audio features (e.g., danceability, energy, valence).

1. Songs with similar audio feature vectors will sound sonically similar and appeal to a user looking for a specific "vibe."

1. Users can articulate the type of song they want to hear using these feature descriptions (e.g., "I want a high-energy, danceable song").

## 4.0 Solution Strategy

This project was developed following a structured data science methodology broken down into the following key steps:

Step 01. Data Description: The project began by loading and examining the Spotify dataset. This initial phase focused on understanding the available features, their data types, and identifying any immediate quality issues like duplicate entries.

Step 02. Exploratory Data Analysis (EDA): An analysis was performed to uncover patterns, relationships, and distributions within the data. This involved visualizing correlations between audio features (e.g., the strong positive correlation between energy and loudness) and understanding the typical range of values for each feature.

Step 03. Machine Learning Modeling: The core of the project involved developing two distinct machine learning models: a content-based recommendation engine to provide personalized suggestions and an unsupervised clustering model to discover hidden sonic groupings within the data.

Step 04. Model Application: The final recommendation model was implemented in an interactive Python script. This script guides the user through the process of selecting a genre, providing their audio preferences, and choosing the number of recommendations they wish to receive, making the model's power accessible to any user.


## 5.0 Top 3 Data Insights

1. Insight 1: Energy and Loudness are Strongly Correlated.
Finding: A strong positive correlation exists between a song's energy level and its loudness (measured in dB). This makes intuitive sense, as songs that are perceived as high-energy are often produced to be louder.


1. Insight 2: Danceability Varies Significantly Across Genres.
Finding: Genres like "Dance," "Pop," and "Hip-Hop" show a much higher average danceability score compared to genres like "Classical" or "Ambient," which have very low scores. This confirms the feature's validity in capturing a key characteristic of a song's style.


1. Insight 3: Most Songs are Not Live Recordings.
Finding: The liveness feature has a distribution that is heavily skewed towards 0. This indicates that the vast majority of tracks in the dataset are studio recordings, with only a small fraction being live performances.


## 6.0 Machine Learning Core

This project implements two distinct machine learning paradigms to analyze and leverage the Spotify dataset: a content-based filtering system for direct recommendations and an unsupervised clustering model for data-driven discovery.

### 6.1 Content-Based Recommendation Engine
This model provides personalized song recommendations by analyzing the intrinsic properties of the music itself.

Methodology: Vector Space Model & Cosine Similarity
The recommendation engine is built on the concept of a Vector Space Model. Each song is represented as a vector in a 10-dimensional space, where each dimension corresponds to a scaled audio feature (danceability, energy, etc.). The user's input is also converted into a vector in this same space.

The core algorithm is Cosine Similarity, which measures the cosine of the angle between the user's vector and every song vector in the dataset. A smaller angle results in a higher cosine similarity score (closer to 1), indicating a stronger sonic match. This geometric approach is highly effective for quantifying similarity in high-dimensional spaces.

Machine Learning Pipeline
Feature Scaling: The StandardScaler from Scikit-learn is applied to the audio features. This is a critical preprocessing step that normalizes the data, ensuring that features with larger ranges (like tempo) do not disproportionately influence the similarity calculation compared to features with smaller ranges (like danceability).

Vectorization: Both the songs and the user's query are treated as vectors.

Similarity Calculation: Cosine similarity is computed between the user's query vector and all song vectors.

Ranking: The songs are ranked in descending order based on their similarity score, and the top N results are returned to the user.

Model Evaluation
The performance of this recommendation system is evaluated qualitatively based on its relevance, ranking, and efficiency:

Relevance: The model consistently returns songs from the correct genre with audio features that closely match the user's numerical input.

Ranking: The recommended songs are returned in a ranked order, with the song having the highest cosine similarity score appearing first.

Efficiency: The model is able to compute and return recommendations from over 170,000 tracks almost instantly.

### 6.2 Unsupervised Learning: Discovering Sonic Clusters
To add a layer of data-driven discovery, an unsupervised learning module was developed to identify natural "sonic clusters" within the dataset. This approach moves beyond traditional genre labels to find inherent groupings of songs based purely on their audio characteristics.

Methodology
Step 1. The Elbow Method: Before clustering, it's crucial to determine the optimal number of clusters. The Elbow Method was used for this. The K-Means algorithm was run for a range of cluster counts (1 to 14), and the inertia (the sum of squared distances of samples to their closest cluster center) was plotted for each. The "elbow" of the plot—the point where the rate of decrease in inertia sharply changes—indicates the most efficient number of clusters. The analysis revealed a clear elbow at k=6.

Step 2. K-Means Clustering: With the optimal k determined, the K-Means algorithm was applied to the scaled audio feature data. Each of the 170,000+ songs was assigned to one of the six clusters based on its sonic profile.

Step 3. Principal Component Analysis (PCA) for Visualization: To visualize these high-dimensional clusters, PCA was used to reduce the 10 audio features into two principal components. These components are new, uncorrelated variables that capture the maximum possible variance in the data. This dimensionality reduction allows the clusters to be plotted on a 2D scatter plot, providing a clear visual representation of their separation and density.

Cluster Profiles and Interpretation
By analyzing the average audio feature values for each cluster, we can define a distinct "sonic identity" or "vibe" for each group.

## 7.0 Project Value
For Users: Provides a powerful tool for music discovery that goes beyond generic playlists. It allows users to find niche songs that perfectly match a specific mood, activity (e.g., workout, study), or creative need.

For a Business (e.g., a Streaming Platform): This system could be integrated to enhance user engagement. It could power a "Create a Vibe" feature for dynamic playlist generation, leading to increased user satisfaction and time spent on the platform.

## 8.0 Conclusions
This project successfully demonstrates the creation of an end-to-end data science application. It proves that a robust and useful recommendation tool can be built by combining data preparation, exploratory analysis, and a core machine learning algorithm. The final interactive script serves as a functional proof-of-concept for a highly personalized music discovery engine.

## 9.0 Lessons Learned
The Importance of Feature Scaling: For any algorithm based on distance or similarity (like Cosine Similarity), standardizing features is a critical step to ensure accurate and unbiased results.

Building for the User: Translating technical feature names into intuitive, easy-to-understand prompts is essential for making a data product usable for a non-technical audience.

Model Simplicity: An effective solution does not always require a complex deep learning model. A well-implemented, traditional algorithm like Cosine Similarity can provide excellent results when applied to the right problem.

## 10.0 Next Steps
Deploy as a Web App: Wrap the application in a web framework like Streamlit or Flask to create a graphical user interface with sliders and buttons.

Incorporate NLP on Lyrics: Fetch song lyrics using an API (e.g., Genius API) and perform sentiment analysis or topic modeling to add lyrical features to the recommendation engine.

