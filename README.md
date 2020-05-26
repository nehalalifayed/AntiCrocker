# AntiCrocker
 AntiCrocker is a website that instructors can use to put exams through filling some simple forms, and have their exam document ready to be printed.
 
 AntiCrocker can grade the exams, by uploading students’ answers to it and based on the model answer a score is given, 
 representing how much the student’s answer is semantically related to the model answer.
 And when grading is done, an excel sheet of students’ grades is saved and ready to be printed anytime, so that the instructor wouldn’t have to write down anything.
 
 # Summary 
 
 Our project consists of two main parts: Generating the exams, and Grading the students’ papers.

Generating the exams : After getting the questions and model answers the instructor enters through the online form, the exam is saved in the DB. After that, all questions are retrieved from the database and python-docx library writes all questions retrieved from the DB, leaving enough space for the student to answer, based on the length of the model answer plus some extra space for him. The exam code and the page number are written in every page of the (.docx) exam. 

Grading Module: After that the instructor can upload the file of the students’ answers for a specific exam, this file will pass first by the OCR module to detect the code of the exam, the student’s name and ID, the questions and the answers. Those answers are passed with the corresponding model answers retrieved from the DB by using the exam code to be graded. The next step is the semantic module that starts to work taking every answer along with the model answer and check the similarity scores using rule-based approaches and ML ones (word2vec Neural Network).

For the rule-based module: The accuracy was 79%.

--we added some extra features:
1. It's known that in some questions numbers are as important as people names to detect if the answer is correct or not, the numbers have high weight as names. 
2.For describing a scene, it is completely different to say "Brown wall and white floor" and "White wall and brown floor", so it was necassary to detect the objects and their related adjectives, also using Spacy library. 
3. Detecting the real subjects and objects of a statement to detect if the student's answer contains the same subjects and objects as the model answer or not, as the student can write the same subject and object but in an order that gives different meaning than that intended in the model answer, using Spacy library. 


For the machine module: 

There were many attempts to use a NN to get the semantic similarity score between two given statements,
and because we needed also to concentrate that the student answer should be compared to the model answer,
we tried to use the well-known siamese NN, with google-news pre-trained embeddings, but it gave very poor accuracy for our task.
So other approaches were made. First we applied the machine learning module on the story questions to use the story pdf/text
to be used as the vocabulary for the embeddings of our semantic NN, as this was our problem with google-news embeddings, 


as it doesn't contain all the vocabulary needed for grading an English Essay Exam. "Gulliver's Travels" was used to be the vocabulary. 
First attempt was by combining glove vocabulary with the vocabulary of the story we have, and with the help of the features extraceted 
from the rule-based module, accuracy was 50%. When using only the vocabulary of the story, with the help of features extracted 
from the rule-based module, accuracy reached 79%. These previous two approaches were made using gensim library. Another approach 
was by just using the features extracted from the rule-based module, but need more time and dataset to be trained.

# Datasets used For the previous trials:
Stanford dataset for training: https://nlp.stanford.edu/projects/snli/

google-news Word2vec embeddings: https://drive.google.com/file/d/0B7XkCwpI5KDYNlNUTTlSS21pQmM/edit

GloVe: https://nlp.stanford.edu/projects/glove/
