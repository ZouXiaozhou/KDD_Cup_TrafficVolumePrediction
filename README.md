# KDD_Cup_TrafficVolumePrediction

This project is the challenge of KDD Cup 2017, in which the participants predict the traffic volume in certain time slots based on traffic volume history.

The raw data record the traffic inspection of three tollgates in a city in China. The tollgate inspects traffic that goes both inbound and outbound. When each car passes a tollgate, following data is recorded: the time, the id of the tollgate, the direction that the car is going and some information of the car such as its type and whether it has etc. A snapshot of raw data is pasted below:

// there should be a snapshot of the raw data

The range of inspection lasts for three weeks. It starts at September 19th and ends at October 17th. The target is to predict the traffic volume for every 20 minutes from 8:00 to 10:00 and from 17:00 to 19:00 in the 4th week, which ranges from October 18th to October 24th. In the prediction period, the traffic volume in every 20 minutes from 6:00 to 8:00 and from 15:00 to 17:00 is given. So the problem can be expressed as predicting the traffic volume in every 20 minutes in the latter 2 hours based on that in every 20 minutes in the former 2 hours. The following figure, referenced from the KDD Cup official website, very well illustrates the target in the prediction period.

// there should be a snapshot of illustration of the problem from KDD Cup website

The submission file should be in the following format:

// there should be a snapshot of the format of the submission

Based on the format of the submission, my team decided to build separate models for each combination of tollage and direction. Since there are 3 tollgates and 2 directions, there are in total 6 models. Although in the training data, the traffic volume within a whole day is provided, because only two hours' data ahead of the prediction period is given in the test set, I also use the four hours' traffic volume given in the test set (6:00 - 8:00 and 15:00 - 17:00) to predict the traffic volume from 8:00 to 10:00 and from 17:00 to 19:00. Though it is certain that there is a better way to make use of the traffic volume in the rest of the day to improve the predictive model, due to the time limit of completing this project, I decide to reduce the complexity of the problem and find a solution that is light-weighted and still very effective. By using a customized K Nearest Neighbor regression algorithm and stacking the result to a decision tree model, I managed to reach this goal.

The customized K Nearest Neighbor regression method works as follows: 

1. Compare the traffic volumes in 6:00-8:00 and 15:00-17:00 (they are given in the test set) in the test set with that in the training set. Find k most similar days in the training set to the test set. Here the similarity is measured by Mean Absolute Percentage Error (MAPE), which is defined as follows:

// there should be a snapshot for MAPE

2. Use th
