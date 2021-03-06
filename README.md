# course-completion-prediction-kaggle
iPython Notebook for CSE 416 Kaggle Competition via https://www.kaggle.com/c/cse-stat-416-sum-20/data

Team name: sophiawhe

Public dataset accuracy: 0.97611

## Methods
- Decision Tree Classifier
- Random Forest Classifier
- AdaBoost Classifier
- K Neighbors Classifier

As a starting point, I chose to use a decision tree classifier. I had practice with decision trees from prior assignments with binary classification, and similarly, this project also required binary classification, as well as because decision trees are fairly efficient. For the decision tree classifier, I tried a small max depth, a mid sized max depth, and a large max depth. Afterward, I tried the two tree-based ensemble methods as well, Random Forest (the sklearn version) and AdaBoost. I thought it would be interesting to compare the various tree-based classifiers we had learned about in class. Finally, I chose K Nearest Neighbors for a distance-based rather than tree-based approach.

## Hyperparameters

- For Decision Tree Classifier: max_depth=5, random_state=1
- For Random Forest Classifier: max_depth=20, random_state=1
- For AdaBoost Classifier: n_estimators=1000, random_state=1
- For K Neighbors Classifier: n_neighbors=4

## Final Choice Model

My final model choice was the Random Forest Classifier, because out of all the models chosen, Random Forest had the best validation data set accuracy.

## Performance

ROC Curves (shown in the notebook) summarize the trade-off between the true positive rate and false positive rate for a predictive model using different probability thresholds. Classifiers that give curves closer to the top-left corner of the plot indicate a better performance, and based on this, the Random Forest classifier has the best performance out of all the models because its curve is closest to the top left. The small decision tree with max depth of 2 has the worst performance, as it is closest to the baseline with no predictive value (farthest from the top left corner out of all the models).

## Feature Selection

The features I used were:

features = [  
    'course_id',            
    'registered',               
    'viewed',                 
    'explored',                
    'LoE_DI',                 
    'YoB',                   
    'gender',                 
    'nevents',                 
    'ndays_act',               
    'nplay_video',            
    'nchapters',             
    'nforum_posts',           
]

- **course id:** institution, course name, semester
- **registered:** 0/1; registered for course = 1
- **viewed:** 0/1; anyone  who accessed  the ‘Courseware’  tab 
- **explored:** 0/1;  anyone  who accessed  at  least half  of  the chapters
- **LoE_DI:** user provided highest level of education
- **YoB:** user provided year of birth
- **gender:** user provided gender m, f, or o
- **nevents:** number of interactions with the course
- **ndays_act:** number of unique days student interacted with course
- **nplay_video:** number of play video  events within the course
- **nchapters:** number of chapters with which the student interacted
- **nforum_posts:** number of posts to the Discussion Forum. 

I chose not to reformat the data for unknowns and decided to keep the 'unk' and -1 representing unknowns as is because I did not want to place any assumptions that would mis-categorize all unknowns for a feature and skew the data. Because many categories had non-numerical data, for preprocessing I used one-hot encoding via the get_dummies() method; though it introduced sparsity into the dataset, it resulted in numerical values for the non-numerical categories.

When analyzing the features used in my final model, the majority of the important features seemed to be non-user-provided features, focusing on the user's interactions with the course and participation. However, some user-provided features were also considered such as highest level of education, year of birth, and gender.

## Predictions
To improve my initial predictions, I first changed my approach from a decision tree classifier to the better-performing random forest classifier. I changed the features to be considered for the model (focusing on removing any possible user-submitted features gradually). I also tuned my random forest max depth hyperparameter, choosing the one that resulted in the best validation data accuracy.
