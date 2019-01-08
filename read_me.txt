{\rtf1\ansi\ansicpg1252\cocoartf1404\cocoasubrtf470
{\fonttbl\f0\fnil\fcharset0 Calibri;}
{\colortbl;\red255\green255\blue255;}
{\*\listtable{\list\listtemplateid1\listhybrid{\listlevel\levelnfc4\levelnfcn4\leveljc0\leveljcn0\levelfollow0\levelstartat1\levelspace360\levelindent0{\*\levelmarker \{lower-alpha\}.}{\leveltext\leveltemplateid1\'02\'00.;}{\levelnumbers\'01;}\fi-360\li720\lin720 }{\listname ;}\listid1}
{\list\listtemplateid2\listhybrid{\listlevel\levelnfc4\levelnfcn4\leveljc0\leveljcn0\levelfollow0\levelstartat1\levelspace360\levelindent0{\*\levelmarker \{lower-alpha\}.}{\leveltext\leveltemplateid101\'02\'00.;}{\levelnumbers\'01;}\fi-360\li720\lin720 }{\listname ;}\listid2}
{\list\listtemplateid3\listhybrid{\listlevel\levelnfc23\levelnfcn23\leveljc0\leveljcn0\levelfollow0\levelstartat2\levelspace360\levelindent0{\*\levelmarker \{disc\}}{\leveltext\leveltemplateid201\'01\uc0\u8226 ;}{\levelnumbers;}\fi-360\li720\lin720 }{\listname ;}\listid3}
{\list\listtemplateid4\listhybrid{\listlevel\levelnfc23\levelnfcn23\leveljc0\leveljcn0\levelfollow0\levelstartat2\levelspace360\levelindent0{\*\levelmarker \{disc\}}{\leveltext\leveltemplateid301\'01\uc0\u8226 ;}{\levelnumbers;}\fi-360\li720\lin720 }{\listname ;}\listid4}
{\list\listtemplateid5\listhybrid{\listlevel\levelnfc23\levelnfcn23\leveljc0\leveljcn0\levelfollow0\levelstartat2\levelspace360\levelindent0{\*\levelmarker \{disc\}}{\leveltext\leveltemplateid401\'01\uc0\u8226 ;}{\levelnumbers;}\fi-360\li720\lin720 }{\listname ;}\listid5}
{\list\listtemplateid6\listhybrid{\listlevel\levelnfc23\levelnfcn23\leveljc0\leveljcn0\levelfollow0\levelstartat2\levelspace360\levelindent0{\*\levelmarker \{disc\}}{\leveltext\leveltemplateid501\'01\uc0\u8226 ;}{\levelnumbers;}\fi-360\li720\lin720 }{\listname ;}\listid6}}
{\*\listoverridetable{\listoverride\listid1\listoverridecount0\ls1}{\listoverride\listid2\listoverridecount0\ls2}{\listoverride\listid3\listoverridecount0\ls3}{\listoverride\listid4\listoverridecount0\ls4}{\listoverride\listid5\listoverridecount0\ls5}{\listoverride\listid6\listoverridecount0\ls6}}
\margl1440\margr1440\vieww10800\viewh8400\viewkind0
\deftab720
\pard\pardeftab720\ri0\sl259\slmult1\sa160\partightenfactor0

\f0\fs22 \cf0 C. B. \
\pard\pardeftab720\ri0\sl259\slmult1\sa160\qc\partightenfactor0
\cf0 \ul \ulc0 Healthcare data modeling\
\pard\pardeftab720\ri0\sl259\slmult1\sa160\partightenfactor0
\cf0 \ulnone Note: You will need to change the name of csv file to the one available in the repo.\
\pard\pardeftab720\ri0\sl259\slmult1\sa160\partightenfactor0

\b \cf0 Browsing the data\
\pard\pardeftab720\ri0\sl259\slmult1\sa160\partightenfactor0

\b0 \cf0 I tried to fit a function to the data I was presented. Prior to doing this, I looked at my data. I retrieved the maximum and minimum values for each column. I also averaged the target value to have an appreciation of the percentage of targets 1 vs. 0. This percentage is 1.72/1000 approximately. \
\pard\pardeftab720\ri0\sl259\slmult1\sa160\partightenfactor0

\b \cf0 Cleaning the data\
\pard\pardeftab720\ri0\sl259\slmult1\sa160\partightenfactor0

\b0 \cf0 I decided as a rule of thumbs to fill the missing values with a value far enough (but not too far) from the minimum value in order to make them outliers, instead of replacing them with the median or mean values. The idea is that the missing values can be informative of a condition (this prevails especially in a medical setting).\
I did not do further cleaning as I do not have much information on the data. The goal was to make the data apt for modelling.\
\pard\pardeftab720\ri0\sl259\slmult1\sa160\partightenfactor0

\b \cf0 Modelling\
\pard\pardeftab720\li720\fi-360\ri0\sl259\slmult1\sa160\partightenfactor0
\ls1\ilvl0\cf0 a-	
\b0 Feature selection \'96 noise reduction\
\pard\pardeftab720\li720\ri0\sl259\slmult1\sa160\partightenfactor0
\cf0 I decided to inquire whether some of the features could be attributed noise. To go quick, I used a random forest classifier with parameters chosen as rule of thumb. I removed the features without which the accuracy would practically not change (or change by an amount less than 10\super 4\nosupersub ) by defining a threshold value of .06 in the selection criteria (select from model). I found the value 0.06 by trial.\
\
\
\pard\pardeftab720\li720\fi-360\ri0\sl259\slmult1\sa160\partightenfactor0
\ls2\ilvl0
\b \cf0 b-	
\b0 Modelling and tuning parameters\
\pard\pardeftab720\li720\ri0\sl259\slmult1\sa160\partightenfactor0
\cf0 After I had found the features I wanted to keep (V2, V10, V11, V14 and V17), I modelled with different function and tuned the parameters to optimize the ROC_AUC and F1 score.  I compared the modelling scores with the ones where all the features where used.\
Because the functions I used evaluate distances to compute the error, I scaled all the values after splitting for training and testing.\
\
\pard\pardeftab720\li1080\fi-360\ri0\sl259\slmult1\sa160\partightenfactor0
\ls3\ilvl0\cf0 -	The logistic regression: \
\pard\pardeftab720\li1080\ri0\sl259\slmult1\sa160\partightenfactor0
\cf0 The logistic regression gave a good ROC_AUC (0.72) score without noise (partial dataset).  \
\pard\pardeftab720\li720\ri0\sl259\slmult1\sa160\partightenfactor0
\cf0         The penalty applied was l1 since I had filtered my data, and the solver I chose was liblinear.\
\pard\pardeftab720\li1080\ri0\sl259\slmult1\sa160\partightenfactor0
\cf0 The score was further improved to .78 by scaling the class inside the logistic function (parameter: class_weight = \'91balanced\'92 instead of default). That way I did not touch the value of the cutoff probability for classification.\
When I used the entire dataset with l2 penalty, the ROC_AUC score was 0.54 . \
\
\
\
\
\pard\pardeftab720\li1080\fi-360\ri0\sl259\slmult1\sa160\partightenfactor0
\ls4\ilvl0\cf0 -	The linear Regression:\
\pard\pardeftab720\li1080\ri0\sl259\slmult1\sa160\partightenfactor0
\cf0 With the intuition the linear regression would probably not be a good model, I ran it quickly without optimization. My AUC was 0.5, very bad, but it could have been due to the rounding of predicted values to accommodate the execution of the codes.\
\pard\pardeftab720\li1080\fi-360\ri0\sl259\slmult1\sa160\partightenfactor0
\ls5\ilvl0\cf0 -	The SVM model\
\pard\pardeftab720\li1080\ri0\sl259\slmult1\sa160\partightenfactor0
\cf0 I used the SVM model on the entire set. I did a gridsearch with nfold cv =5 to optimize the parameter gamma (How far the model has an influence) and C (for simplicity of the model, no over fitting). I could not reach an AUC value of .70. The time of execution increased drastically. It took too long to obtain a response.\
I ran my model with the filtered data set and reduced the computational time. I also optimized the AUC to .91 and the F1score to .64, which is pretty decent. However the values of C and gamma for optimization were the largest of the grid. Is there over-fitting? (yet we have filtered the data).\
\
\pard\pardeftab720\li1080\fi-360\ri0\sl259\slmult1\sa160\partightenfactor0
\ls6\ilvl0\cf0 -	The MLP classifier\
\pard\pardeftab720\li1080\ri0\sl259\slmult1\sa160\partightenfactor0
\cf0 I used the MLP classifier because of the power of the neural network on the filtered data set. I operated a gridsearch with hidden layers [7, 4] and [30, 20] (neurons or nodes and layers).  The raw data gave an ROC_AUC of .52. The filtered data gave a ROC_AUC of 0.66\
with solver lbfgs.\
\pard\pardeftab720\ri0\sl259\slmult1\sa160\partightenfactor0
\cf0 Using the random forest tree for a quick feature selection and then fitting, testing and tuning with the logistic regression model and SVM were the best solution (good ROC_AUC and F1 scores). The k-fold gridsearch with SVM gave good results, however the gamma and C values were the largest and for the logistic regression the penalty l1 was used (because the date were filtered). \
\
}