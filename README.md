# Code: A classification of social media comments based on controversial statement characteristics

This repository holds the code to my bachelor thesis for the study-program 
*Creative Computing*. The topic of the thesis was to identify features 
that represent if a social media comment is controversial or not. The given comments
are classified by these determined features.

# Experimental Setup
In the following the process for getting to the final result will be explained. To try the 
code yourself you would need to apply for the full DeTox-dataset and place it at `detox/DeTox-Dataset_complete.sqlite3`.

## 01: Modify data structure
In a first step the given data-structure was transformed into a format appropriate for the use case.
For each comment that had a conversation-id assigned the next two comment-texts of the conversation are each added 
as a property to the comment. This is done to have a better overview of the conversation and to be able to evaluate
if the reactions to a comment are of a different opinion or not. The resulting data-structure is saved as a CSV-file.
The available columns in the end are:
- c_id
- c_text
- date
- conv_id
- reaction1
- reaction2

## 02: Pre-processing annotated comments
The annotated comments are modified to be easier to work with in a machine learning model. 
The text of the main-comment as well as the reactions where modified.
The modifications where:
- Removing all mentions (strings starting with "@")
- Removing links (starts with "http")
- Removing all line-breaks and duplicated white-spaces
- Removing occurrences of character codes (like "&amp;")

The table structure was modified in the way, that a separate column was added for any of the four values the 
_Generalisation_ could take on, and the original column was removed.

The annotated comments are saved in three different CSV files:
- **04_comments_annotated-no_reaction.csv**: One for all comments without any reaction related data
- **04_comments_annotated-reactions.csv**: One for all comments with a reaction and the corresponding data
- **04_comments_annotated-values.csv**: All comments that where annotated with all their columns

## 03: Training and evaluating the model
A model for predicting features that are indicating a controversial comment is fine-tuned. As a pre-trained model the
_multilingual DistilBERT base cased_ (distilbert-base-multilingual-cased) model is used. 
The fine-tuning is performed with the `transformers`-library and _PyTorch_. 

1. First the dataset is read from the CSV-file, the specific tuples for the final validation are removed from the dataset, unnecessary columns are dropped.
2. Global variables for the training process are defined.
3. The dataset structure for the model is defined.
4. The dataset is split into a training and a validation set.
5. A customised model class, as well as functions for saving and loading the model state are created.
   - In this all the layers that are added onto the pre-trained model for fine-tuning are defined.
   - In this case the additional layers are:
     - A linear layer
     - A dropout layer
     - A linear layer
     - A sigmoid layer
6. The model is trained and evaluated. During the training process various metrics are logged and saved. The best model is saved.
   - The loss-function is weighting the classes, as the dataset is imbalanced. More weight is given to the classes in minority.
     Without this weighting the model would predict the majority class for every comment and ignore any classification on the minority classes.
7. The best model is loaded from disk and evaluated on the test set.
8. The results of the final-test set are saved in a CSV-file.

The model was created with the help of the following resources:
- https://huggingface.co/docs/transformers/v4.17.0/en/tasks/sequence_classification, retrieved on 19.02.2024
- https://huggingface.co/docs/transformers/en/training, retrieved on 19.02.2024
- https://www.youtube.com/watch?v=TmT-sKxovb0, retrieved on 19.02.2024
- https://www.youtube.com/watch?v=f-86-HcYYi8, retrieved on 19.02.2024
- https://colab.research.google.com/github/DhavalTaunk08/Transformers_scripts/blob/master/Transformers_multilabel_distilbert.ipynb#scrollTo=zHxRRzqpBf76, retrieved on 19.02.2024
- https://huggingface.co/docs/transformers/model_doc/distilbert#usage-tips, retrieved on 19.02.2024

# Acknowledgements
The dataset used in this thesis is the [Detox](https://github.com/hdaSprachtechnologie/detox)-dataset 
which was presented in Demus et al. (2022, pp. 143–153). 

Demus, C., Pitz, J., Schütz, M., Probol, N., Siegel, M., & Labudde, D. (2022). Detox: A
comprehensive dataset for German offensive language and conversation analysis.
Proceedings of the Sixth Workshop on Online Abuse and Harms (WOAH), 143–153. https://doi.org/10.18653/v1/2022.woah-1.14

# Contact
**Vanessa Köck** \
💻 www.vanessakoeck.dev \
📧 me@vanessakoeck.dev
