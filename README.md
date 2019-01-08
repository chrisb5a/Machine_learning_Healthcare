# Machine_learning_Healthcare
140 MB file
Healthcare data modeling
Note: You will need to change the name of csv file to the one available in the repo.

-Browsing the data

-I tried to fit a function to the data I was presented. Prior to doing this, I looked at my data. I retrieved the maximum and minimum values for each column. I also averaged the target value to have an appreciation of the percentage of targets 1 vs. 0. This percentage is 1.72/1000 approximately. 

-Cleaning the data

I decided as a rule of thumbs to fill the missing values with a value far enough (but not too far) from the minimum value in order to make them outliers, instead of replacing them with the median or mean values. The idea is that the missing values can be informative of a condition (this prevails especially in a medical setting).

I did not do further cleaning as I do not have much information on the data. The goal was to make the data apt for modelling.

-Modelling

a-	Feature selection – noise reduction

I decided to inquire whether some of the features could be attributed noise. To go quick, I used a random forest classifier with parameters chosen as rule of thumb. I removed the features without which the accuracy would practically not change (or change by an amount less than 104) by defining a threshold value of .06 in the selection criteria (select from model). I found the value 0.06 by trial.


b-	Modelling and tuning parameters

After I had found the features I wanted to keep (V2, V10, V11, V14 and V17), I modelled with different function and tuned the parameters to optimize the ROC_AUC and F1 score.  I compared the modelling scores with the ones where all the features where used.
Because the functions I used evaluate distances to compute the error, I scaled all the values after splitting for training and testing.

-	The logistic regression: 

The logistic regression gave a good ROC_AUC (0.72) score without noise (partial dataset).  
        The penalty applied was l1 since I had filtered my data, and the solver I chose was liblinear.
The score was further improved to .78 by scaling the class inside the logistic function (parameter: class_weight = ‘balanced’ instead of default). That way I did not touch the value of the cutoff probability for classification.
When I used the entire dataset with l2 penalty, the ROC_AUC score was 0.54 . 


-	The linear Regression:

With the intuition the linear regression would probably not be a good model, I ran it quickly without optimization. My AUC was 0.5, very bad, but it could have been due to the rounding of predicted values to accommodate the execution of the codes.

-	The SVM model:

I used the SVM model on the entire set. I did a gridsearch with nfold cv =5 to optimize the parameter gamma (How far the model has an influence) and C (for simplicity of the model, no over fitting). I could not reach an AUC value of .70. The time of execution increased drastically. It took too long to obtain a response.
I ran my model with the filtered data set and reduced the computational time. I also optimized the AUC to .91 and the F1score to .64, which is pretty decent. However the values of C and gamma for optimization were the largest of the grid. Is there over-fitting? (yet we have filtered the data).

-	The MLP classifier:

I used the MLP classifier because of the power of the neural network on the filtered data set. I operated a gridsearch with hidden layers [7, 4] and [30, 20] (neurons or nodes and layers).  The raw data gave an ROC_AUC of .52. The filtered data gave a ROC_AUC of 0.66
with solver lbfgs.
Using the random forest tree for a quick feature selection and then fitting, testing and tuning with the logistic regression model and SVM were the best solution (good ROC_AUC and F1 scores). The k-fold gridsearch with SVM gave good results, however the gamma and C values were the largest and for the logistic regression the penalty l1 was used (because the date were filtered). 

