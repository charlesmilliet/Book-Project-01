***
# NYT Bestseller Search & Quiz
«NYT Bestseller Search & Quiz» is a project created in the context of the course “Programming with advanced computer languages” by Dr. Mario Silic in the spring semester 2021 at the University St. Gallen. The program allows users to search and filter the NYT bestsellers database and to test his knowledge in a quiz on bestseller books. The project used the Python programming language and dataset used was on the «New York Times Bestseller list» between 2010 and 2019, which is available on Kaggle for free: (https://www.kaggle.com/dhruvildave/new-york-times-best-sellers).
***

## Table of contents
* [General Information](#general-information)
* [Technologies](#technologies)
* [Install packages](#install-packages)
* [Data preparation](#data-preparation)
* [Program Structure](#program-structure)
* [Authors](#authors)

## General Information
The programme aims at providing users with a quick option to search for bestsellers based on various categories, such as title, author name, date on bestseller list, weeks on bestseller list, and price. Furthermore, the programme should help users to test and expand their knowledge on bestsellers through a short, but entertaining quiz. 
	
## Technologies
Python Version: 3.8.5
Jupyter Notebook: To install Jupyter Notebook, please refer to https://jupyter.org/install.
	
## Install packages
Libraries used: `pandas` `numpy` `datetime` `os` `dateutil.relativedelta` `random` 
To install libraries in python, run the command `pip install "package name"`, for example see jupyter notebook script.

## Data preparation
In order to be able to use the datafile for our program, we made the following adjustments. We loaded the original date into a pandas dataframe and then deleted the columns “list_name_encoded”,  “list_name, rank”, “isbn13”,  “isbn10”,  “amazon_product_url”, as we do not need the data included here for our program.  Some lines in the original data included a comma so we decided to separate the columns with ‘;’ and replaced any ‘;’ included in the actual data (for more details on this, please refer to the respective notebook).
Following, we have removed all duplicates in the data frame and sorted the rows by alphabetical order. Duplicates stem from the fact that books which are many weeks on the NYT bestseller list will be listed on the data frame each time the book was published again on the NYT bestseller list. We keep the first release date and the maximal amount of weeks on the bestseller list for each duplicates. All other information is repeated so it does not matter which one is kept.
The dataset has six columns that are: “title”, “published_date”, “author”, “description”, “price”, and “week_on_list” and contains 6577 observations. The clean data frame is saved as a txt file separated by “;” called “NYTB_clean.csv”.
For further details, check the notebook “raw_data_NYTB”.

## Program Structure

### 00 - Initialization
Import packages used: pandas numpy datetime dateutil.relativedelta random
### 01 - Data
After importing the csv file, an empty list is created. Every line in the csv is then added as a new list to the main list. Every object in every line of the csv file is its own item in one of the sublists. Data types are adjusted to fit the content, e.g. transformation to a date format. The main list serves as the dataset which will be used throughout the project. 
### 02 - Basic Functions
Below is an overview of the basic function used to search the bestseller list dataset. 
#### 02.1 - Display Functions
The res_search function displays the results of all the search functions introduced below. It prints the title, author, first time the book was on the bestseller list, time on the bestseller list, and price for matching books.
Should there be more than five matches, only the first five are printed. The user is informed if this is the case. Should there be no matches, and thus the results list is empty, the user is informed that no book matches its search input. 
The function display_n_books allows the user to see any desired number of books, not just the first five. 
#### 02.2 - Search by Title
The search_by_title function requests a title input from the user. It then loops through all book titles in the dataset. Every matching book is added to a new list containing all the results. If there are no matches, this list remains empty.
The programme automatically ignores capitalisation in the user input. Furthermore, it is not only possible to search books by their full title, but also by title fragments only. 
#### 02.3 - Search by Author
The search_by_author function requests an author name as input from the user. It then loops through all authors in the dataset. Every book by a  matching author is added to a new list containing all the results. If there are no matches, this list remains empty.
The programme automatically ignores capitalisation in the user input. Furthermore, it is not only possible to search books by full author name, but also by name fragments. 
#### 02.4 - Search by Date
The search_by_date function requests two dates as input between which a book should be on the bestseller list from the user and then loops through the dataset.  Every book with a matching date is added to a new list containing the results. If there are no matches, the list remains empty.
The input must be in formats of YYYY, YYYY-MM, or YYYY-MM-DD. The user is prompted to use the correct format, else an error message occurs. The program requires users to enter a start date earlier than the end date, otherwise an error message will occur. If two times the same date is entered, an exact match will be looked for. 
#### 02.5 - Search by Number of Weeks on Bestseller List
The week_NYTB function requests input from users on the minimal number of weeks a book should have been on the bestseller list. Then the function loops through all books in the dataset. Every book that meets the time threshold will be added to a list containing all the results. An empty list will be returned if no book meets the threshold of time on the bestseller list.
The programme checks if the user input is an integer, else an error message is displayed. If a user wants all books displayed, a 0 can be entered. 
#### 02.6 - Search by Book Price
The search_by_price function requests from the user two numbers between which the price of the book should fall. The function then loops through all books to see which ones fit into the price range. Every matching book is added to the list of results. If there are no matches the result list remains empty. 
The order of the two prices between which the books should fall does not matter, as the programme automatically adjusts for that. Furthermore, the code checks if both inputs are numbers. Else, an error message is displayed. 
### 03 - Advanced Search Functions
The search_select function allows the user to select according to which parameter the dataset should be filtered. Once a criterion is selected, the respective search function is triggered. The user also has the option to quit the programme. If an invalid input is entered, an error message occurs. 
The function adv_search triggers the search_select function. However, it also allows the user to make searches using several filters at the same time. 
### 04 - Quiz Function
The function quiz allows the user to test its bestseller knowledge in a fun and entertaining way. Points can be collected for every question that has been rightly answered throughout several rounds. Users can decide on the number of rounds they want to play and will start with 0 points for the quiz.  For wrong answers, 30 points are deducted up to a score of zero points. 
There are four types of questions. They either ask for the author, time on the bestseller list, or the bestseller year of a specific book, or they ask for which book was written by a specific author. For every question, four answer possibilities are displayed, out of which exactly one is correct.  A fifth option removes one wrong answer, however then less points are awarded for selecting the correct answer. 
The function works as follows. A while loop is running until the user decides to quit the game. Every question of the quiz happens as a round in a for loop. For every question a type is determined randomly. Then, a book at random is selected for the question to be based on. The correct solution is extracted based on the question type. Furthermore, three wrong answers are generated by randomly selecting answer possibilities out of the dataset which are distinct from each other and the correct answer. All four answer possibilities are added to a list and shuffled before being presented to the user together with the question. The user can then select the question which is deemed correct. 
If the answer is correct, points are added, the score is displayed,  and the next question is randomly generated until the final round is completed. If it is incorrect, points are deducted and the next question is randomly generated. After the final round the final score is displayed and the user is asked if another game of the quiz should be started. If this is the case, the points are reset and the for loop which generates questions is started again. If the user does not want to play another round, the while loop breaks and the quiz mode ends. 
### 05 - Final Project
The final project combines all the above mentioned functions. It starts with a function asking the user what he wants to do by giving the users three options, which are search by criteria, advanced search and quiz. Based on the selection, the relevant functions are run. The user also has the option to quit the programme. 


## Authors
Charles Milliet

Jannis Braun

Jinshi Cai

Charlotte Mast

