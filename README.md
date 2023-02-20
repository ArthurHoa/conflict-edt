# Conflict EDT
A python version of an Evidential Decision Tree based on a conflict measure.

### Summary

When the data are labeled in an uncertain and imprecise way, Evidential Decision Tree models can be used for classification problems.
The model presented here uses conflict as a splitting criterion.

### Reference

When using this code please cite and refer to [Paper being published](https://github.com/ArthurHoa/conflict_edt)

### Example

For two observations respectively labeled *I think it's a dog* and *I'm sure it's a cat*, the model will try to group the observations in two different nodes. After the construction of the tree, a new observation will then be classified according to its attributes.


### How to use

Initialize the model:
```
classifier = EDT()
```

Train the model on the training set, with the attrributes *X_train* and the labels *y_train* defined on $2^M$, with *M* the number of classes :
```
classifier.fit(X_train, y_train)
```

Use score to predict the classes of *X_test*, compare them to *y_test* and return the accuracy of the model:
```
precisions = classifier.score(X_test, y_test)
```

## Example on Credal Dog-4

### Credal Dog-4

Link to the dataset : [Credal Dog-4](https://github.com/ArthurHoa/credal-datasets)

Foxhound | Basset | Brittany | Beagle
:--:|:--:|:--:|:--:
<img src="https://github.com/ArthurHoa/credal-datasets/blob/master/ressources/pictures/Foxhound.jpg?raw=true" width="70"> | <img src="https://github.com/ArthurHoa/credal-datasets/blob/master/ressources/pictures/Basset.jpg?raw=true" width="70"> | <img src="https://github.com/ArthurHoa/credal-datasets/blob/master/ressources/pictures/Brittany.jpg?raw=true" width="70"> |  <img src="https://github.com/ArthurHoa/credal-datasets/blob/master/ressources/pictures/Beagle.jpg?raw=true" width="70">  

### Code

```
from sklearn.model_selection import train_test_split
from decision_tree_imperfect import EDT
import numpy as np

X = np.loadtxt('X.csv', delimiter=';')
y = np.loadtxt('y.csv', delimiter=';')
y_true = np.loadtxt('y_true.csv', delimiter=';')

indexes = [i for i in range(X.shape[0])]
train, test, _, _ = train_test_split(indexes, indexes, test_size=.2)

classifier = EDT()

classifier.fit(X[train], y[train])

precision = classifier.score(X[test], y_true[test])

print("Accuracy : ", precision)
```

Accuracy = 0.61

### Output of the model

An exmaple of the Evidential Decision Tree prediction for the following picture is given as follows:

<img src="https://www.dropbox.com/s/f67s7jwie1tnfs1/72.jpg?raw=true" width="150">  
  
Prediction:  
m({Basset}) = 0.71  
m({Foxhound, Basset}) = 0.12  
m({Foxhound, Basset, Beagle, Brittany}) = 0.17  
  
True class: Basset
