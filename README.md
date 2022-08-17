# Book-Recommendation-System
**A fullstack(ish) data science project to build a book recommendation system using Collaborative Filtering (Machine Learning) where Top 4 books will be recommendated to user upon input.**

This project aims to create a book recommendation system. It will target many areas of data science. At a high level, the steps are:

1. **Cleaning** and **pre-processing** data (take scraped data and make it more useful)
2. **Explore** data (understand the scraped data)
3. Build **classifier model** system (create a recommendation system based on data)
4. **Deploy** system (create a web service using the model)

## 1. Data Cleaning and Pre-Processing

The dataset consists of three tables; **Books**, **Users**, and **Ratings**. Data from all three tables are cleaned and preprocessed separately as defined below briefly:

For **Books** Table:

* Drop all three Image URL features.
* Check for the number of null values in each column. There comes only 3 null values in the table. Replace these three empty cells with ‘Other’.
* Check for the unique years of publications. Two values in the year column are publishers. Also, for three tuples name of the author of the book was merged with the title of the book. Manually set the values for these three above obtained tuples for each of their features using the ISBN of the book.
* Convert the type of the years of publications feature to the integer.
* By keeping the range of valid years as less than 2022 and not 0, replace all invalid years with the mode of the publications that is 2002.
* Upper-casing all the alphabets present in the ISBN column and removal of duplicate rows from the table.

For **Users** Table:

* Check for null values in the table. The Age column has more than 1 lakh null values.
* Check for unique values present in the Age column. There are many invalid ages present like 0 or 244.
* By keeping the valid age range of readers as 10 to 80 replace null values and invalid ages in the Age column with the mean of valid ages.
* The location column has 3 values city, state, and country. These are split into 3 different columns named; City, State, and Country respectively. In the case of null value, ‘other’ has been assigned as the entity value.
* Removal of duplicate entries from the table.

For **Ratings** Table:

* Check for null values in the table.
* Check for Rating column and User-ID column to be an integer.
* Removal of punctuation from ISBN column values and if that resulting ISBN is available in the book dataset only then considering else drop that entity.
* Upper-casing all the alphabets present in the ISBN column.
* Removal of duplicate entries from the table.

## 2. Algorithms Implemented:
### 2.1 Popularity Based Recommendation :
Popular in the **Whole** Collection : We have sorted the dataset **according to the total ratings** each of the books have received in non-increasing order and then recommended **top 50 books**.

![1](https://user-images.githubusercontent.com/91668225/185101385-4e710af1-0beb-49db-8e73-66f5e1aaf87a.gif)


### 2.2 Recommendation using Average Weighted Rating
We have calculated the weighted score using the below formula for all the books and recommended the books with the **highest score**.

                                                   score= t/(t+m)∗a + m/(m+t)∗c

where,
t represents the **total number of ratings** received by the book

m represents the **minimum** number of total ratings considered to be included

a represents the **average rating** of the book and,

c represents the **mean rating** of all the books.

### 2.3 User-Item Collaborative Filtering Recommendation
Collaborative Filtering Recommendation System works by considering user ratings and finds **cosine similarities** in ratings by several users to recommend books. To implement this, we took only those books' data that have at **least 50 ratings** in all.

### 2.4 Correlation Based Recommendation
For this model, we have created the **correlation matrix** considering only those books which have total ratings of more than 50. Then a user-book rating matrix is created. For the input book using the correlation matrix, top books are recommended.

### 2.5 Nearest Neighbour Based Recommendation
To train the Nearest Neighbours model, we have created a compressed sparse row matrix taking ratings of each Book by each User individually. This matrix is used to train the Nearest Neighbours model and then to find n nearest neighbors using the **cosine similarity metric**.

### 2.6 Content Based Recommendation
This system recommends books by calculating similarities in Book Titles. For this, **TF-IDF feature vectors** were created for unigrams and bigrams of Book-Titles; only those books' data has been considered which are having at least 80 ratings.

## 3. Libraries Used:
* ipython-notebook - Python Text Editor
* sklearn - Machine learning library
* numpy, scipy- number python library
* pandas - data handling library
    
## 4. Deployment : 
This project uses **Flask** as web API and **Heroku** as web server for deployment.

Check out mu project  : https://book-recomm-sys.herokuapp.com/


![2](https://user-images.githubusercontent.com/91668225/185101290-a4f1fda6-7f30-462c-a7d3-c7716c50e5f8.gif)

