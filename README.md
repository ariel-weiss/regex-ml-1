# regex-ml

## Table of Contents:
- [About](#about)
- [Installation](#installation)
- [Resources](#resources)
- [The Project Process](#process)
- [Files](#files)
- [How to use](#howto)
- [Key Functions](#functions)

<a name="about"/>

## About:

<br>This project tested whether using machine learning tools might be useful in tasks of information tagging. Part of a larger project, “The Jewish Book Closet”, it focuses on tagging references of hebrew sources, in this case, the Babylonian Talmud. In the past, regular expressions were used for the task of finding these references, but they have proven difficult to work with, especially with Hebrew sources, and therefore a machine learning approach was tested. One of the more difficult steps when working with machine learning is the creation of a large enough data set for the machine to learn from. Our purpose was to create that data set using weak supervision machine learning methods. 

<br>The tool creates a labeled data set which will contain short sequences of an input text, and determine which is a reference to the Babylonian Talmud and which is not: <br>The program receives a CSV file as input, breaks it into sentences, and then breaks each sentence into sequences in a range of sizes (can be changed). Using Snorkel and Pandas Python libraries, it uses predecided (manually) labeling functions to label the sequences and create the tagged data set.

<br>The working process showed that the task at hand was much easier than it was using only regular expressions, especially when dealing with Hebrew sources. Most importantly, it resulted in a large tagged data set, which would have been impossible to create manually. In order to test if data set is satisfactory for a machine to learn from, we created a basic classifer using the data set, and checked it on a small test set. The next step is to take the data set this tool creates to train a classifer that will tag any input text. We believe that with further understanding of existing tools in Deep learning it will be possible to achieve even better and meaningful results.

<br> For detailed information about the project, go to the wiki page📚📜.

<a name="installation"/>

## Installation guidelines

<br>In order to run this project, you'll need python version 3.7.1.
<br>Install the requirements from the requirements file:
```
pip install -r requirements.txt
```
If you run in trouble with torch installation, try installing it manually, then install the requirements:
```
pip install torch===1.1.0 torchvision===0.3.0 -f https://download.pytorch.org/whl/torch_stable.html

pip install -r requirements.txt
```

<a name="resources"/>

## Resources
<br> https://www.snorkel.org/
<br> https://scikit-learn.org/
<br> https://jakevdp.github.io/PythonDataScienceHandbook/

<a name="process"/>

## Project Process
<br>The process consisted of three steps:
- First, creating a labeled data set - preparing the data set involved extraction of the text from a csv file, deviding it by sentences into ngrams of different sizes, creating the labeling functions and labeling using Snorkel Majority Label Voter model. Also, it involved cleaning the resulting labels from unnecessary duplications which using different ngram sizes may have caused. 
- Second, using transformations on the tagged dataset to enlarge it - the transformation were based on replacing masachtot and masachtot chapter names.
- Third, training the classifier - training the classifier using the Logistic Regression linear model (scikit learn), with
the labeled data set we have created as input.

 ### Clarifications
 
<br> <br>Examples of a reference to the Babylonian Talmud: 
>**":ובפרק תינוקת (ברכות דף ס"ט)"**
<br>How werethe Labeling Functions decided? by perliminary manual overview of examples of references to the the Babylonian Talmud.
<br>Why was the n-gram format chosen? seemed most adequate and allowed us to include different sizes of references. That since we aspire that the tagging will be as acurate as possible, therefore we go over different n-gram sizes.

<a name="files"/>

## Files of this project

<br>The project consists of the following files:
<br>[main.py](main.py) - the main part of the project, includes the labeled data creation and training of the classifier
<br>[labeled_function.py](labeled_function.py) – contains the labeling functions and their description.
<br>[transformation_functions.py](transformation_function.py) - contains the transformation functions used to increase the labeled data set
<br>[utility.py](utility.py) – contains utility functions such as text parsing.
<br>Data directory:
<br> - contains the [analysis file](data/analysis.txt) - contains output analysis for every run, of functions coverage and classifier accuracy.
<br> - [csvRes](data/csvRes.csv) - name of expected input text in csv format. 
<br> - [df_test.csv](data/df_test.csv) and df_train.csv - 30-70 split of labeled data used to train the classifier
<br> - [labeled_data](data/labeled_data.csv) - outputed labeled data
<br>  - [labeled_data_augmented.csv](data/labeled_data_augmented.csv) - outputed labeled data including additions of transformation functions. 

 <a name="howto"/>
 
 ## How to use this project:
 
1. 🍴 Fork or 👯 Clone this repo to your local machine.
2. Take the input file (Hebrew text of course) and turn it into CSV file,  name it "csvRes.csv" and put it in the Data directory.
3. Set the following constants which appear in the [utility file](utility.py) -
* <b>SAMPLE_SIZE</b> : the number of rows to use from the csv file.
* <b>MIN_N_GRAM_SIZE</b> and <b>MAX_N_GRAM_SIZE</b> : determines the range of n-gram sizes.
* <b>TRANSFORMATION_FACTOR</b> : determines the number of transformation of each label which contains a masechet or masechet chapter  name. It needs to be between 0 and number of total masachtot/prakim.
* <b>TEST_RATIO</b> = 0.30 : how to split train and test datasets for the classifier training.
4. Run [main.py](main.py) .
5. Check the results at the [analysis file](data/analysis.txt) and explore 🔨 

 <a name="functions"/>
 
 ## important functions
 
 <br>In [main.py](main.py):
* load_labeled_data - extracts ngrams from the csv input file
* apply_lf_on_data - appplies the labeling functions on the data set and tags them
* apply_tf_on_data - applies the transformation functions on the labeled data set
* train_model - trains the classifier and outputs results
 ---
 <br> For further explanation, check out the [Snorkel website](https://www.snorkel.org/) mentioned under resources. Consider changing the labeling and transformation functions if see it fit.
 <br>The main function calls for several important functions which purpose is described thoroughly in the code.
 <br> good luck!
 
