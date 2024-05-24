# Exploratory Data Analysis (EDA) on Flight Prices

## Introduction

The airline industry has seen a steady rise in popularity over the years as air travel has become more accessible and affordable to the average person. With the increase in demand, airlines have had to be more competitive with their pricing strategies to attract and retain customers. In this project, we will be exploring a flight price dataset obtained from Kaggle and using it to predict flight prices.

## About Dataset

The flight price dataset contains information on flight prices, departure and arrival times, the airline, the duration of the flight, and the source and destination airports. The dataset is in CSV format and contains purchasable tickets available on Expedia for flights between 16th April 2022 and 5th October 2022, to and from 16 airports which are of ATL, DFW, DEN, ORD, LAX, CLT, MIA, JFK, EWR, SFO, DTW, BOS, PHL, LGA, IAD, OAK. Each row in the dataset represents a single ticket. The dataset contains information about flights, including details about the itinerary, fare, and availability of seats.

The size of the dataset is 28.9 GB. 
Here is s a brief explanation of the columns in the dataset - 

legId: An identifier for the flight. This is a unique value assigned to each leg of a trip, which is a portion of the journey between two airports. A single trip can have multiple legs, each with its own leg ID.

searchDate: The date (YYYY-MM-DD) on which this entry was taken from Expedia. This column specifies the date when the search was conducted on Expedia for the given itinerary.

flightDate: The date (YYYY-MM-DD) of the flight. This column specifies the date of the actual flight.

startingAirport: Three-character IATA airport code for the initial location. This column specifies the IATA code of the airport from where the flight is scheduled to depart.

destinationAirport: Three-character IATA airport code for the arrival location. This column specifies the IATA code of the airport where the flight is scheduled to arrive.

fareBasisCode: The fare basis code. This column represents a code that indicates the fare rules and restrictions that apply to a particular ticket.

travelDuration: The travel duration in hours and minutes. This column represents the duration of the flight from the departure time to the arrival time.

elapsedDays: The number of elapsed days (usually 0). This column represents the number of days between the search date and the flight date.

isBasicEconomy: Boolean for whether the ticket is for basic economy. This column represents whether the ticket is of basic economy type or not.

isRefundable: Boolean for whether the ticket is refundable. This column represents whether the ticket is refundable or not.

isNonStop: Boolean for whether the flight is non-stop. This column represents whether the flight is non-stop or not.

baseFare: The price of the ticket (in USD). This column represents the base fare price of the ticket, which does not include taxes and fees.

totalFare: The price of the ticket (in USD) including taxes and other fees. This column represents the total fare price of the ticket, which includes taxes and fees.

seatsRemaining: Integer for the number of seats remaining. This column represents the number of seats that are still available for purchase on the flight.

totalTravelDistance: The total travel distance in miles. This data is sometimes missing. This column represents the total travel distance of the flight in miles.

segmentsDepartureTimeEpochSeconds: String containing the departure time (Unix time) for each leg of the trip. The entries for each of the legs are separated by '||'. This column represents the Unix time of the departure of each leg of the trip.

segmentsDepartureTimeRaw: String containing the departure time (ISO 8601 format: YYYY-MM-DDThh:mm:ss.000±[hh]:00) for each leg of the trip. The entries for each of the legs are separated by '||’. This column represents the departure time of each leg of the trip in ISO 8601 format.

segmentsArrivalTimeEpochSeconds: String containing the arrival time (Unix time) for each leg of the trip. The entries for each of the legs are separated by '||'. This column represents the Unix time of the arrival of each leg of the trip.
There is information of 16 airports altogether in the dataset. 

## Steps to perform Dataset loading and Preparation

We have installed PySpark library using pip and imported necessary modules from PySpark and pandas. We have also created a SparkSession with the application name "FlightPricesEDA" to manage the Spark application. Additionally, we have mounted the Google Drive using the Colab notebook to access the dataset stored in the CSV file. Finally, we have loaded the dataset from the CSV file using SparkSession's read method by providing the path to the CSV file, specifying the header to be true, and inferring the schema of the dataset automatically.

We have checked the number of rows and columns in the dataset using the count() method on the DataFrame object and the len() function on the columns of the DataFrame object. We have also checked for missing values using the select() method and count() function from PySpark SQL functions. We have used the dropDuplicates() method to remove duplicate rows from the dataset and printed the number of duplicates before and after removing them. Finally, we have assigned the modified DataFrame to the variable 'df' for further analysis.
Operations performed on the dataset (EDA)  

We have analysed the summary statistics of numerical variables in the dataset using the describe() method of the DataFrame object. We have provided the names of the columns we are interested in as a list parameter. The method returns the count, mean, standard deviation, minimum, and maximum values for the given columns. We have used this information to gain insights into the distribution of values in the dataset and to identify any potential outliers. The results have been displayed in a tabular format using the show() method.
 
We have explored the categorical variables in the dataset using the groupBy() and agg() methods of the DataFrame object. We have grouped the data by each categorical variable and used the count() function to calculate the frequency of each category. We have then assigned an alias to the count column and sorted the data in descending order using the orderBy() method on the count column. We have done this for StartingAirport, destinationAirport, segmentsAirlineName, segmentsAirlineCode, and segmentsCabinCode. This has allowed us to gain insights into the distribution of categorical variables in the dataset and identify any patterns or anomalies in the data. The results have been displayed in a tabular format using the show() method.–       

 
We have calculated the average fare prices for each airline in the dataset using the groupBy() and agg() methods of the DataFrame object. We have grouped the data by segmentsAirlineName and used the avg() function to calculate the average baseFare and totalFare for each airline. We have then assigned an alias to each calculated column to improve the readability of the output. Finally, we have sorted the data in descending order by the average baseFare using the orderBy() method on the avgBaseFare column. This analysis has allowed us to gain insights into the pricing strategies of each airline and identify any potential outliers or anomalies in the data. The results have been displayed in a tabular format using the show() method.
 

We have calculated the number of flights between each airport pair in the dataset using the groupBy() and agg() methods of the DataFrame object. We have grouped the data by startingAirport and destinationAirport and used the count() function to calculate the number of flights between each airport pair. We have then assigned an alias to the count column and sorted the data in descending order using the orderBy() method on the count column. This analysis has allowed us to gain insights into the most popular airport pairs and identify any potential trends or patterns in the data. The results have been displayed in a tabular format using the show() method.
 
We have calculated the percentage of basic economy tickets sold, refundable and nonstop tickets using the groupBy() and agg() methods of the DataFrame object. We have grouped the data by the isBasicEconomy column and used the count() function to calculate the number of occurrences for each value. We have then assigned an alias to the count column and calculated the percentage of each category by dividing the count by the total number of rows in the dataset and multiplying by 100. Finally, we have displayed the results in a tabular format using the show() method. This analysis has provided us with insights into the distribution of different ticket types in the dataset and helped us identify any trends or patterns in the data. 

## Plotted Histogram of baseFare and totalFare: 

We have modified the code that was using PySpark.Pandas library to plot histograms of 'baseFare' and 'totalFare'. Instead, we have used the simpler Pandas library to convert the PySpark DataFrame to a Pandas DataFrame. Then, we have plotted the histograms using the seaborn library and displayed them using the matplotlib library. The resulting plots are identical to the ones generated by the original code, but with fewer dependencies and a simpler code structure.
 
we have created a boxplot for the base fare and total fare using PySpark and the Seaborn library. We first imported the necessary libraries, including Matplotlib, Seaborn, and PySpark Pandas. We then converted the PySpark DataFrame to PySpark Pandas DataFrame, which allowed us to use Seaborn to create the boxplot. We specified the x-axis data for the boxplot and assigned each plot to a separate axis. Finally, we used the plt.show() function to display the plots. The resulting boxplots provide a visual representation of the distribution of data for the base fare and total fare variables, highlighting their quartile ranges, median, and outliers.
 

## Boxplot of baseFare for each airline: 

The PySpark code that we have implemented can generate a box plot of the base fare for each airline in a provided dataset. Initially, the code selects the distinct airline names from the dataset and creates a flattened list of airline names by utilizing the `flatMap()` method. It then filters the dataset to select rows with a specific airline name, extracts the base fare data using the `select()` method, and converts it into a Pandas DataFrame. This process is repeated for each airline, and the base fare data is collected as a list of Pandas DataFrames. Eventually, the code utilizes Matplotlib to plot the box plot. This method is scalable and appropriate for big data applications because it can perform parallel processing on vast datasets. In summary, our PySpark code offers a distributed and scalable solution for generating box plots of base fares for each airline in a provided dataset.

## Histogram of travelDuration:
The PySpark code that we have implemented generates a histogram of travel durations in a given dataset. Firstly, the code selects the travel duration column from the dataset and converts it to a Pandas DataFrame. Then, the code uses the histogram() method to calculate the frequency distribution of the travel durations, with the specified number of bins, and returns a tuple of two lists representing the bin edges and frequencies. The collect() method is then used to retrieve these lists from the RDD and Matplotlib is utilized to plot the histogram. Finally, the code sets the axis labels and displays the histogram using the show() method. This approach enables us to perform histogram analysis on large datasets in a distributed and scalable manner. In summary, the PySpark code provides a scalable and distributed solution for generating histograms of travel durations in a given dataset.

## Scatter plot between baseFare and totalFare:

Implemented machine learning algorithms on the dataset:
Linear Regression and Decision Tree regression:

These are the results after applying the machine learning algorithms.

## Scatter plot between baseFare and totalFare:
The PySpark code that we have implemented generates a scatter plot between base fare and total fare in a given dataset. Firstly, the code selects the base fare and total fare columns from the dataset and converts them to Pandas DataFrames. Then, the scatter() method is used to plot the scatter plot with the base fare on the x-axis and the total fare on the y-axis. The code sets the axis labels and displays the scatter plot using the show() method. This approach enables us to perform scatter plot analysis on large datasets in a distributed and scalable manner. In summary, the PySpark code provides a scalable and distributed solution for generating scatter plots between base fare and total fare in a given dataset.
 
## Implemented machine learning algorithms on the dataset:
The PySpark code that we have implemented performs regression analysis using linear regression and decision tree regression models on a given dataset. Firstly, the code selects the numeric columns "baseFare" and "totalFare" and creates a feature vector using the VectorAssembler class. The code splits the data into training and testing sets using the randomSplit() method. The code then standardizes the features using the StandardScaler class. The PySpark code then creates two regression models: linear regression and decision tree regression. The models are fitted to the training data using the fit() method. The PySpark code then evaluates the models on the test data using the RegressionEvaluator class with the root mean squared error (RMSE) metric. The RMSE values for linear regression and decision tree regression are printed using the print() function. This approach provides a scalable and distributed solution for performing regression analysis on large datasets in a distributed and scalable manner. In summary, the PySpark code provides a scalable and distributed solution for performing regression analysis on a given dataset using linear regression and decision tree regression models.
 
## Conclusion
Based on the analysis performed on the flight price dataset, we can conclude that:
- The dataset contains information about flights, including details about the itinerary, fare, and availability of seats.
- The average base fare and average total fare can be calculated based on the airlines.
- The dataset can be analyzed using summary statistics and visualization techniques such as histograms, boxplots, and scatter plots.
- Machine learning algorithms such as Linear Regression and Decision Tree Regression can be applied to predict flight prices.
- The accuracy of the machine learning models can be improved by tuning the hyperparameters.
Overall, this analysis provides insights into the flight pricing strategies used by airlines and can be useful for predicting flight prices and making informed decisions about air travel.


.


