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
- id
- c_id
- c_text
- date
- conv_id
- reaction1
- reaction2

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
