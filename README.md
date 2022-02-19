This repository corresponds to a simple project to manipulate some retail data from an Excel file and output some relevant information through different plots and analysis of dataframes.

From a dataset with several transactions spanning from 2010 to 2011, across multiple countries and several invoices and products, our goal is to import this dataset inside a MongoDB via a python program.
Then, we will set up and use Apache Spark in order to manipulate the data.

For an easier way, we will use a single jupyter notebook to manipulate the data and present some results from it.
You can already see the results from the notebook or run it again and modify as you wish for the information required.

#### Prerequisites
This code was made under Windows 10. As we didn't test under Linux, we cannot confirm all functionalities will work under Linux.

We assume the following are already installed and ready to use:
* Java SDK 11.0
* Apache Spark
* Docker Desktop
* python3.8

As we are importing the dataset to MongoDB, it is required to have access to a MongoDB.
In our case, we used a local installation of MongoDB to create a new database.
But to avoid installing MongoDB, the same process was done and tested on another computer using a docker image for MongoDB (There are just 2 lines to adapt in notebook for it, see comments in it).

To use a docker image of MongoDB, you simply need to execute the following commands in a command prompt:
```
docker run --name mongodb -v mongodata:/data/db -d -p 27017:27017 mongo
docker exec -it mongodb bash
```
When done using Mongo, simply stop the docker
```
docker stop mongodb
docker rm mongodb
```

Next time, you will need to access MongoDB simply execute again the docker as explained above (all information added in MongoDB in previous session will be kept)

#### Start the project
As explained above, while the prerequisites are installed, we would like to execute the simple jupyter notebook **demo.ipynb**.
For it, we provided the python packages requirements so you can either install it on your default python but we recommend to use a virtualenv for it and then apply:
```
pip install -r requirements.txt
```
You can then simply start jupyter notebook by executing the command:
```
jupyter notebook
```
Then, open the notebook **demo.ipynb**


#### Next steps
As explained in the notebook, some improvements can still be done.
* To share the results with a Marketing department, the plots need to be improved. As there are a lot of different products, they should be grouped by categories and then we should extract the distribution per category over countries.
* European Community and Unspecified countries were not managed in the World Map plot, we should include them as additional information
* The dataset was quite incomplete (missing somme price unit, some invoices, some clients, ...). Here we decided to ignore this incomplete data but it can be useful to extract it in order to improve the acqquisition procedure for next time
* The display of World map of transactions per countries is not kept in jupyter notebook and we cannot fix this bug. To avoid loading it each time, we find a countermeasure by saving this map in **map.html** file (but this html does not display the popup, so it's still better to run notebook)
* As explained in last section in notebook, the product should be grouped in categories to apply some NLP solution over description. For it, few steps are required:
    * Prepare a training dataset, by annotating manually as corresponding categories a part of the dataset
    * Implement an NLP algorithm
    * Train over training dataset and apply inference over testing dataset
    * Group by categories of products