# Swiss Geography Master - Learn Switzerland's Geography with Python
Hi there! You just found the student project "Swiss Geography Master", which is part of the course "Programming with Advanced Computer Languages" by Mario Silic (Autumn Semester 2020 at the University of St. Gallen). The result of this project is a fun game built with Python to learn more about Switzerland in a few minutes and to improve your knowledge of Switzerland's geography! If this intrigues you, please read on and get more information!

## Table of contents
* [General Information](#general-information)
* [Technologies](#technologies)
* [Setup](#setup)
* [Program Structure](#program-structure)
* [Authors](#authors)
* [Appendix - Libraries Description](#appendix---libraries-description)

## General Information
The goal of this project is to increase the general awareness of Switzerland's geography and to entertainingly teach the user some fun facts and numbers about the country. The program shows on the map where the cantons' capitals and other Swiss landmarks are located and gives the user an intuition about how populated each canton is. The program is divided into multiple chapters and it transitions from a learning section to a game section. For simplicity, in the whole code we refer to the user as "user" or "he", and under the pronouns "he", "him", and "his" we include every gender.
	
## Technologies
* Python version: 3.8.3
* Jupyter Notebook: To install Juypter Notebook, please refer to https://jupyter.org/install
* Libraries used: `pandas`, `numpy`, `locale`, `folium`, `random`, `tkinter`, `json`, `math` (for their descriptions refer to [Appendix - Libraries Description](#appendix---libraries-description))
	
## Setup
To run this program, it is recommended to use Jupyter Notebook/Anaconda. Additionally, it is necessary to have installed the above listed libraries. If not installed yet or if not already part of the Anaconda distribution, please install them locally with PowerShell by Anaconda giving the appropriate commands as in the following examples:

```
$ pip install folium
$ pip install pandas
$ pip install tkinter
```
Before running the program, it is fundamental to export and save locally all the files that are collected on this GitHub repository (code, Excel files, figures, ...), or the program will be incomplete and will show errors. 

## Program Structure

### Chapter 0: Import data and packages
As introduction step, the user imports the packages and the data. This is important for the rest of the code to run correctly and without errors.
* Packages to import: `pandas`, `numpy`, `locale`, `folium`, `random`, `tkinter`, `json`, `math`
* Data to import: `Population.xlsx`, `Coordinates.xlsx`. The data in those tables are needed for the further illustration purpose of the map. The data includes the population numbers for the cantons and all coordinates for the pointers (capitals and landmarks).

### Chapter 1: Preliminary steps to create the map
In this chapter the code prepares and defines the functions and the objects necessary to later create the map, where the user finds the locations of the Swiss cantons' capitals and of some Swiss landmarks. To show the map the program uses the `folium` package. To create the markers on the map the program uses the `.Marker` function. When the user clicks on the marker of a capital, a message appears with the population of the respective canton. This section prepares and prints the text messages of the markers.

### Chapter 2: Creation of map and markers
This section is responsible for the display of the map, the markers, and the popup messages. The code starts with the creation of the markers in `folium`.

The markers need the following elements:
* Coordinates: These are collected in the file `Coordinates.xlsx`. We find and import the latitude and longitude data from the fourth and fifth column, respectively.
* Popup: This is the message that appears when the user clicks on the tooltip of the marker. The code creates a list of sentences for the popup messages. For ease of reading, the popup is defined with the `folium.Popup()` function outside of the `folium.Marker()` function. The size of the popup box results from the use of `max_width=` and `min_width=`.
* Icon: For aesthetic reasons the program creates visually pleasing icons (background information can be obtained with the `help(folium.Icon)` function). The definition of the icon prints the information sign "i" and two different colours.

The code displays markers in red for the cantons' capitals and in blue for the landmarks. For the landmarks, it is possible to adjust the function dynamically to account for further new inputs. This means that when a new landmark is added to the list, the map updates itself automatically (by counting the numbers of "non-canton-objects" and appending them to the loop function).

The final result is therefore an interactive and informative map, where the user can click on different locations and gain information.

### Chapter 3: Location warm-up
This chapter creates a small pre-quiz and tests the user about the locations of the cantons' capitals. The answers are then shown on the map for further study.

First, the code creates a list of two random cities with the `random` package and the `random.sample` command. With the sample command the program selects 2 elements out of the range of the number of cantons. The two random cantons are stored in the random list with numbers between 0 and 25.

Then, the code creates the game with rules, score, and memory of the user's input. The program checks the answer of the user with an `if` function (only the following inputs are accepted: "E,W,S,N").

Finally, the score is printed using the `sum` function on our score list, and the two selected cities are shown on the map for a visual check.

### Chapter 4: Last check before the game
The user is given a last chance to check for some capitals on the map before the game starts. The code explains the procedure to the user and shows the coordinates dataframe. To avoid confusion the program only selects the rows with the cities in the data frame with the `.iloc` command.

Furthermore, the user is asked to input the number of capitals that he would like to check and also to input the abbreviations of the interested cantons. For the sake of this, the program needs a dictionary that allocates the right number with the corresponding canton's name. The dictionary finds which abbreviation is in which row. That way, the code reads a number even though the user enters the abbreviation of the canton.

At the end, the program displays the new map with only the user's choices.

### Chapter 5: Final quiz with GUI!
The user is then ready to start playing the game. The code creates a quiz on a GUI (Graphical User Interface) with a total of 30 different questions. In each round the program randomly extracts 5 questions for the user to answer. The maximum score achievable of each round is 5 points (one for each question).

The quiz code has been taken from a youtube tutorial (https://www.youtube.com/watch?v=ES8GDaBbgEI&t=1s). The basics were already given with a start page and start button. Further, the quiz pages with the multiple choices and at the end a page with a funny cartoon were already part of the game.

Our group amends the following points in the quiz:
* Basics: Start page image, start button, final page cartoons, size, titles, fonts, quiz questions, points given for each correct answer.
* Added value: Show final score of the user, "Play Again" button, "Exit" button, overview of the questions asked with their correct answers.

The "Play Again" button is introduced at the end of the game and destroys all of the graphics on the final page, resets the randomized list of the questions and the score, and brings the user back to the first question of the game (calling function `startquiz`).

The "Exit" button is also introduced at the end of the game and destroys the whole game. It just exercises the function `game.destroy`. 

At the end of the quiz, we show the final score of the user and the overview of the questions asked with their correct answers.

Give it a try and we hope you like the Swiss Geography Master! 

## Authors
Zachary Matteucci

Filippo Coduri

Nina Tuchschmid




## Appendix - Libraries Description

##### Pandas:
`pandas` is an open-source, BSD licensed library that enables the provision of easy data structure and quicker data analysis for Python. For operations like data analysis and modelling, `pandas` makes it possible to carry these out without needing to switch to more domain-specific language like R. Support for operations such as re-indexing, iteration, sorting, aggregations, concatenations and visualizations are among the feature highlights of `pandas`. 

##### NumPy:
`numpy` is one of the fundamental Python packages for scientific computing, as it provides support for large multidimensional arrays and matrices along with a collection of high-level mathematical functions to execute these functions swiftly. This interface can be utilized for expressing images, sound waves, and other binary raw streams as an array of real numbers in N-dimensional. `numpy` can also be used as an efficient multi-dimensional container of generic data. 

##### Locale: 
The `locale` module is part of Python’s internationalization and localization support library. It provides a standard way to handle operations that may depend on the language or location of a user. For example, it handles formatting numbers as currency, comparing strings for sorting, and working with dates. 

##### Folium: 
The `folium` library builds on the data wrangling strengths of the Python ecosystem and the mapping strengths of the `leaflet.js` library. `folium` makes it easy to visualize data that’s been manipulated in Python on an interactive leaflet map. It enables both the binding of data to a map for `choropleth` visualizations as well as passing rich vector/raster/HTML visualizations as markers on the map. The fact that the `folium` results are interactive makes this library very useful for dashboard building. 

##### Random:
The `random` module implements pseudo-random number generators for various distributions. Almost all module functions depend on the basic function `random()`, which generates a random float uniformly in the semi-open range [0.0, 1.0). 

##### Tkinter:
The `tkinter` package (“Tk interface”) is the standard Python interface to the Tk GUI toolkit (Graphical User Interface). When Python is combined with the `tkinter` library, it provides a fast and easy way to create GUI applications. In these applications `tkinter` provides various controls, such as buttons, labels and text boxes. 

##### Json:
JavaScript Object Notation (JSON) is a standardized format commonly used to transfer data as text that can be sent over a network. The `json` library can parse JSON from strings or files. The library parses JSON into a Python dictionary or list. It can also convert Python dictionaries or lists into JSON strings.

##### Math:
The `math` module is a standard module in Python and is always available. The library provides access to the mathematical functions defined by the C standard. All methods of this functions are used for integer or real type objects, not for complex numbers.


