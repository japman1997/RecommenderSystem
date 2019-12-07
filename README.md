# RecommenderSystem

Abstract: 
Recommender systems are algorithms designed to help users discover movies, products, and songs by predicting the user’s rating of each item and displaying similar items that they might rate high as well. The objective is to show customers content that they would like best based on their historical activity. 
The system will recommend movies to the users as per their interest as well as it will recommend movies rated by other users who are similar to the user.

### DATASET 1 : MOVIE
- MovieID : non-null Integer id distinct to every movie
- Title : non-null String, Name of the Movie
- Genres : non-null String, Type of the Movie

### DATASET 2 : RATING
- UserID : non-null Integer id distinct to every user
- MovieID : non-null Integer id distinct to every movie
- Rating : non-null Float value (1-5) (1 being the lowest and 5 being the highest)
- Timestamp : non-null Integer showing time 

Since Timestamp in the rating dataset doesn’t contribute much in the recommendation process, we can drop that attribute thus saving both space and time in processing.

Since we cannot work on 2 different datasets to calculate the similarity, thus combing the datasets based on the movieId attribute as this is the only attribute common in both the datasets. Using the merge function from the panadas library, we were able to create a single dataset to work with.

#### Working with Pivot Table. 
Pivot table is a function to create Create a spreadsheet-style pivot table as a DataFrame. The levels in the pivot table will be stored in MultiIndex objects (hierarchical indexes) on the index and columns of the result DataFrame. In the paper, we passed three parameters in the pivot table function. Those are
- Index
- Columns 
- Values

In Index and columns if an array is passed, it must be the same length as the data. The list can contain any of the other types (except list). Keys to group by on the pivot table index. If an array is passed, it is being used as the same manner as column values. In index we pass the userId, in columns we pass the movie name or the title and, in the values, we pass the ratings thus creating a whole matrix of user vs movie names and ratings as the data of it. The shape of this pivot table is 610,9722.

#### Correlation
Compute pairwise correlation between rows or columns of DataFrame with rows or columns of Series or DataFrame. DataFrames are first aligned along both axes before computing the correlations. Using the corrwith [8] function from pandas with a specific movie which returns a series of titles that are correlated with that movie based on the ratings. There could be a lot of null values in the series. We can put that series in a Dataframe and then join the count of the ratings to that dataframe to get an idea. 
The next step is to remove the null values from the dataframe as there could be a lot of movies that have no correlation with that movie. Sorting them in the descending order, we can observe the movies which are positively related to that specific movie. To get a better accuracy on if the movie is actually related to the specific movie, we can make sure that the count of the votes should be more than at least 5. This way we would know that at least 5 people have voted that this movie is of a specific type.
