# NLP_couse_project
For this assignment, I tried to create an auto response email message for the user. However, I was unsuccessful with this project. 
Overall, I imported comments and emails, preprosseced them and tried making seq2seq as my model1 and then for model2 I use cos sim to find the most sim comment to the prediction.



I first imported reddit comments from bigquery and place them into a dataframe where it will me easier to read them. Next I place all the comments in to a list called comments. 
From there I created a method that filters out the comments that would be inappropriate for email response and I filtered out the comments. Also filitered out comments with more than 75 characters. Because I had limited time to complete this assignment, I only took 5000 comments of the 70000.
After that, I preprossed the comments that has been filitered and put them in a list called filtered_comments. I also created a list of all of the unquie words from the comments called vocab.
Then I created 2 dict where i loop through vocab and each word will have an index and in the second dic every index has a word. 

I then created a pretrained word2vec model.
I created a method called compute_vector_avg in which it will return the average vector of the text. In compute_vector_avg the text is preprossed and then I spilt the text into words and loop through each word and add each vector together. If the model is unable to coveret the word to a vector than just ingore the word. After looping divide by the total vec by amount of words, if the text has no words at all in the model than just return an array of zeros 
Next I created a method called index_dic, in this method I loop through the comments and find the cosine simmilarty betwwen them. if the comments is higher than .85 than add than comment in the same index. The purpose of this method is group simiar comments to lesson the amount of comments there are. At the end the method returns a dic where the keys a numbers and the values are a list of comments.

Then I import things read the emails. I loop through maildir which has a lot of emails and I split them into list where if there is a response to the emails it will be in one list if not that place it in a differrnt list. I am only taking the email body's and also the first 40000 emails.
First I preproccessed the emails with replies. i split each email body that has Original  or fowarding message. From there I loop throgh that email and preproccessed by removing the hraders and removing extra spaces, etc. I append the that email in to a list then once the loop is done I append that list into a list. This will make to be a 2d list where in every list it will be the emails and the responses sepereately. 
Next I preproccessed the emails with no replies 
I created a stop word methos that is not being used 
I then loop through the 2d list of emails reply (emails_filtered_replies) and added the email to the as a key and the reply would be the value. For example: [[email3, email2, email1], [email2.1, email1.1] ...] - > [[email1, email2, email3], [email1.1, email2.1] ...] -> { email1:email2, email2:email3, email1.1:email2.1, ....} (but I am converting each list one by one not all at the same time)

I then create a method called convert_vec weher it take a the a text and convert the text into a vec where if text is in vocab than place a 1 else the vec would be a 0
(My program kept crashing so I took the first 1000 words)
I then bulid my x and y train for my model1, using the cos sim, I try to find a similar comment to the email replies and ry to replace that reply to the email if it not the sim at all than I just use the the email reply I use the convert_vec to covert to a vec and add it to the y train. My x train is the key of the reply that also has been converted to a a vec by using convert_vec
I then build my gru model and and trainedd it for 51 emails because I had linited time, I then try to decode it but it did not work I did however did get a preditve output. 

I then try to make a new model. 
I created a new x and y train where again I take replies with lower than 100 characters and I still use cos sim to find the comments to replace the email replies but intead of using the vocab list to create a vector I use the average vector as my x and y train. 
Then I created a built a different model and train the model. I then test the model where for my prediction I try to find the most similar comment using cos sim for that prediction and if the under .5 than print no response as a way to say the email will have no reply 
