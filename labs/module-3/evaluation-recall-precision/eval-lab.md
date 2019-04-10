
# Using the evaluation metrics we have learned, we are going to compare how well some different types of classifiers perform on different evaluation metrics

#### We are going to use a dataset of written numbers which we can import from sklearn
import numpy as np
from sklean.datasets import fetch_mldata
mnist = fetch_mldata('MNIST original')
X, y = mnist['data'], mnist['target']

#### Take a look at the shapes of the X and y matricies 
X.shape()
y.shape()

#### Now, let's pick one entry and see what number is written. Use indexing to pick the 36000th digit 
some_digit = X[36000]

#### You can use the .reshape(28,28) function and plt.imshow() function with the parameters cmap = matplotlib.cm.binary, interpolation="nearest" to make a plot of the number. Be sure to import matplotlib!
import matplotlib
import matplotlib.pyplot as plt 
some_digit_image = some_digit.reshape(28,28)
plt.imshow(some_digit_image, cmap = matplotlib.cm.binary, interpolation="nearest")
plt.axis("off")
plt.show()

#### Use indexing to see if what the plot shows matches with the outcome of the 36000th index
y[36000]

#### Now lets break into a test train split to run a classification. Instead of using sklearn, use indexing to select the first 60000 entries for the training, and the rest for training
X_train, X_test, y_train, y_test = X[:60000], X[60000:], y[:60000], y[60000:]

#### We are going to make a two-class classifier, so lets restrict to just one number, for example 5s. Do this by defining a new y training and y testing sets for just the number 5
y_train_5 = (y_train == 5) 
y_test_5 = (y_test == 5)


#### Lets train a logistic regression to predict if a number is a 5 or not (remember to use the 'just 5s' y training set!)
from sklearn.linear_model import LogisticRegression
lr = LogisticRegression()
lr.fit(X_train, y_train_5)

#### Does the classifier predict correctly the 36000th digit we picked before?
lr.predict([some_digit])



#### To make some comparisons, we are going to make a very dumb classifier, that never predicts 5s. Build the classifier with the code below, and call it using: never_5_clf = Never5Classifier()
from sklearn.base import BaseEstimator
class Never5Classifier(BaseEstimator):
 def fit(self, X, y=None):
 pass
 def predict(self, X):
 return np.zeros((len(X), 1), dtype=bool)
never_5_clf = Never5Classifier()

#### Now lets fit and predict on the testing set using our never 5 Classifier
never_5_clf.fit(X_train, y_train_5)
never_5_preds = never_5_clf.predict(X_test)

#### Let's compare this to the Logistic Regression. Examine the confusion matrix, precision, recall, and f1_scores for each. What is the cutoff you are using?
lrpreds = lr.predict(X_test)

from sklearn.metrics import confusion_matrix, precision_score, recall_score, f1_score
#Never 5
confusion_matrix(y_train_5, never_5_preds)
precision_score(y_train_5, never_5_preds) 
recall_score(y_train_5, never_5_preds) 
f1_score(y_train_5, never_5_preds)

#Logistic Reg
confusion_matrix(y_train_5, lrpreds)
precision_score(y_train_5, lrpreds) 
recall_score(y_train_5, lrpreds) 
f1_score(y_train_5, lrpreds)


#### What are the differences you see? Without knowing what each model is, what can these metrics tell you about how well each works?

#### Now let's examine the roc_curve for each. Use the roc_curve method from sklearn.metrics to help plot the curve for each
from sklearn.metrics import roc_curve
fpr, tpr, thresholds = roc_curve(y_train_5, y_scores)

def plot_roc_curve(fpr, tpr, label=None):
 plt.plot(fpr, tpr, linewidth=2, label=label)
 plt.plot([0, 1], [0, 1], 'k--')
 plt.axis([0, 1, 0, 1])
 plt.xlabel('False Positive Rate')
 plt.ylabel('True Positive Rate')

plot_roc_curve(fpr, tpr)
plt.show()

#### Now find the roc_auc_score for each. 
from sklearn.metrics import roc_auc_score
roc_auc_score(y_train_5, y_scores)

#### What does this metric tell you? Which classifier works better with this metric in mind?





