# Potential Talents

The goal of this project is to predict how fit the candidates are based on their available information. Rank candidates based on a fitness score and then Re-rank candidates when a candidate is starred.

#Data Description:

 a unique identifier is gived for each candidate.

Attributes:
id : unique identifier for candidate (numeric)

job_title : job title for candidate (text)

location : geographical location for candidate (text)

connections: number of connections candidate has, 500+ means over 500 (text)

Output (desired target):
fit - how fit the candidate is for the role? (numeric, probability between 0-1)

Keywords: “Aspiring human resources” or “seeking human resources”

#Approach
I did the text pre-processing of the the job-title column which  have the key words.
Create doc2vec embeddings of "Aspiring human resources" (w1) and also for each job_titles and calculate cosine similarity between the embeddings.
Convert the "connection" column as a numeric column then scale the connection column from 0-1 (maybe by using minmaxscaler).
Created a column (ranking) which is weighted sum of cosine_similarity and scaled_connection. Giving higher weightage to similarity.
Based on the ranking column, sorted the dataframe in descending order and the top n candidates will be the candidates which are more relevant.

I  repeated the same steps by adding bert embeddings and elmo embeddings for "Aspiring human resources" and also for each job_titles.
BERT technique is more effective for ranking the talents and would be adopted. It's performance is because it's pretrained large corpus of unlabelled text.

#Re-ranking
After starring a candidate(s) by entering the id, the job titles of that candidate(s) becomes the keyword and then the pointwise technique would be used to re-rank the talent list to select the potential talents.

Re-rank using the job title starred as keyword and finding its cosine similarity to all the other job titles. For this task Bert Embeddings vectors will be used.


Finally I trained a lightGBM Ranking Algorithm using the consine simiralities of all the embeddings and the model had an accuracy of 90.o1% after hyperparameter tuning.

