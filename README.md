# cost-optimising-cloud-job-scheduling

The dependancies Boto3, Pandas, MatPlotLib and Numpy will need installing using pip before you will be able to run any scripts.

Part 1 - Price Comparision and Evaluation

** After installing the dependancies just run the comparePrices.py script, see explaination of scripts below 

The first part of the application consists of the scripts comparePrices.py, priceEval.py and AWSData.py:

The AWSData.py file contains a large array of the spot instance types, regions and availability zones and is used by the other part one scripts.

The comparePrices.py script takes instance specification constraints from the user via the command line such as memory, ECU units etc and then filters the instances. Parrallism is then used to compare the varying region and availability zones prices of each viable spot instance type so that the cheapest region and availability zone to host in at the current time for each instance type is known.

Then based on the specification bias the user selected in the beginning such as for cpu or memory etc. all of the lowest instance type prices will then be ranked based on cost divided by which ever specification bias was selected to return the instance ranked at number one for best price vs cpu or best price vs memory etc. This instance which is regarded as best value for money at the current time given the user's initial specification constraints is then passed on to functions in the priceEval.py script.

The priceEval.py script is reponsible for looking at the current price of an instance with respect to portion of its past prices in order to ensure that the current price is not outside of the third quartile. Ensuring the current price is not a high outlier is performed as verification, as well as because there is a highly likelihood that the price will lower if we wait when the price is a high outlier. This allows to program to decide whether to wait and re-loop the previous step to check for price change or to execute and launch the spot instances now.

To Do:
- Make each region and availability price look up parrallel instead of just each instance type
- Remove instance storage option use EBS only
