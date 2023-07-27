# DC_DA
The objective of this project is to conduct a social media experiment and analyze the engagement patterns of various categories of tweets. We will generate random tweet data for different categories, analyze the distribution of likes, and compute statistics to understand the average likes for each category.

### Importing required librabries
import random
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
get_ipython().run_line_magic('matplotlib', 'inline')
import seaborn as sns

### Generated random data for social media data and categorizing
df = pd.read_csv("C:\\Users\\DELL\\Cost of living tweets.csv")

df.head()

df.shape

df.info()

categories = ['date_time', 'username', 'user_location', 'follower_count', 'following_count', 'tweet_like_count', 'tweet_reply_count', 'tweet_text']

n_periods = 500                                                              # Define the list of categories, number of periods

start_date = '2022-01-01'

dates = pd.date_range(start=start_date, periods=n_periods)                   # Generate random dates within a specific date range

random_categories = [random.choice(categories) for _ in range(n_periods)]    # Generate random categories using random.choice()

random_likes = np.random.randint(0, 10000, size=n_periods)                   # Generate random integers for the number of likes

data = {
    'Date': dates,
    'Category': random_categories,
    'Likes': random_likes
}                                                                            # Create the data dictionary with Date, Category, and Likes

tweet_data = pd.DataFrame(data)                                              # Create a DataFrame from the data dictionary

print(tweet_data)

### Load the data into Pandas Dataframe and Explore the data

categories = ['date_time', 'username', 'user_location', 'follower_count', 'following_count', 'tweet_like_count', 'tweet_reply_count', 'tweet_text']

n_periods = 500

start_date = '2022-01-01'

dates = pd.date_range(start=start_date, periods=n_periods)

random_categories = [random.choice(categories) for _ in range(n_periods)]

random_likes = np.random.randint(0, 10000, size=n_periods)

data = {
    'Date': dates,
    'Category': random_categories,
    'Likes': random_likes
}

tweet_data = pd.DataFrame(data)                           # Create a DataFrame from the data dictionary

print("DataFrame Head:")
print(tweet_data.head())                                  # Print the DataFrame head (first few rows)

print("\nDataFrame Information:")
print(tweet_data.info())                                  # Print the DataFrame information

print("\nDataFrame Description:")
print(tweet_data.describe())                              # Print the DataFrame description (summary statistics)

print("\nCount of each 'Category' element:")
print(tweet_data['Category'].value_counts())              # Print the count of each 'Category' element

### Perform necessary data cleaning steps to remove null data, remove duplicates

categories = ['date_time', 'username', 'user_location', 'follower_count', 'following_count', 'tweet_like_count', 'tweet_reply_count', 'tweet_text']

n_periods = 500

start_date = '2022-01-01'

dates = pd.date_range(start=start_date, periods=n_periods)

random_categories = [random.choice(categories) for _ in range(n_periods)]

random_likes = np.random.randint(0, 10000, size=n_periods)

data = {
    'Date': dates,
    'Category': random_categories,
    'Likes': random_likes
}

tweet_data = pd.DataFrame(data)
tweet_data.dropna(inplace=True)                                   # Data Cleaning Steps

tweet_data.drop_duplicates(inplace=True)                          # Remove duplicates (if any) 

tweet_data['Date'] = pd.to_datetime(tweet_data['Date'])           # Convert 'Date' to datetime format

tweet_data['Likes'] = tweet_data['Likes'].astype(int)             # Convert 'Likes' to integers

print("Cleaned DataFrame Head:")
print(tweet_data.head())

print("\nCleaned DataFrame Information:")
print(tweet_data.info())

print("\nCleaned DataFrame Description:")
print(tweet_data.describe())

print("\nCount of each 'Category' element:")
print(tweet_data['Category'].value_counts())

###  Visualize likes data and create a histogram plot by using seaborn library

plt.figure(figsize=(10, 6))                                                     #Create a boxplot using seaborn
sns.histplot(data=tweet_data, x='Likes', kde=True, bins=30, color='blue')
plt.title('Histogram of Likes')
plt.xlabel('Likes')
plt.ylabel('Frequency')
plt.show()                                                                      #Show the boxplot

### To visualize the distribution of likes for each category and create a boxplot with x-axis as 'Category' and y-axis as 'Likes' by using seaborn boxplot() function

plt.figure(figsize=(10, 6))

sns.boxplot(x='Category', y='Likes', data=tweet_data, palette='pastel')

plt.title('Boxplot of Likes by Category')

plt.xlabel('Category')

plt.ylabel('Likes')

plt.xticks(rotation=45)                                                      #Rotate the x-axis labels for better readability

plt.show()

### Perform some statistics on the likes data(Mean of 'likes' category using groupby() method)

mean_likes = tweet_data['Likes'].mean()                                  #Calculate and print the mean of the 'Likes' category

print("Mean of 'Likes' category:", mean_likes)

mean_likes_by_category = tweet_data.groupby('Category')['Likes'].mean()  # Group by Category and calculate the mean of each category 'Likes'

print("\nMean of 'Likes' for each Category:")

print(mean_likes_by_category)
