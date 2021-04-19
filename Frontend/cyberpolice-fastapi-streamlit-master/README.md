## CYBERPOLICE : using FASTAPI and STREAMLIT

### Images
![Negative - not sexually harassing](./images/negative.png)
![Positive - sexually harassing](./images/positive.png)

#### Note:
- This is a simple ML webapp accompanying the research in https://github.com/whopriyam/Sexual-Harassment-Classification.
- The application is found to be computationally very expensive and hence the application could not be deployed online using free resources.


### About the application
[CyberPolice](https://github.com/whopriyam/Sexual-Harassment-Classification) is a simple ML webapp built using FastAPI, Streamlit, Docker and docker-compose.

The [project](https://github.com/whopriyam/Sexual-Harassment-Classification) determined that BERT proved to be the best algorithm for detecting if texts are sexually harassing or not.

The application uses BERT model trained on a dataset of sexually harassing tweets to detect sexual harassment in texts.
##### Project Structure

* backend/
  * models/
    * *saved_model_name/*
  * `Dockerfile`
  * `__init__.py`
  * `config.py`
  * `main.py`
  * `requirements.txt`
* frontend/
  * `Dockerfile`
  * `__init__.py`
  * `main.py`
  * `requirements.txt`
* jupyter_notebooks/
  * `Export_Model_Weights_Bert_SH.ipynb`
* storage/
* `.gitignore`
* `LICENSE`
* `README.md`
* `docker-compose.yml`


##### To run the application

 - Run the python notebook in `jupyter_notebooks/` directory on Google Colab with GPU hardware acceleration enabled.
 - Upon completion, from the Colab file side menu, download the zip file containing the model weights generated by the python notebook.
 - Extract the zip file inside the `backend/models/` folder. The pretrained model weights are now saved in this directory.
 - Change the variables as required in `backend/config.py`.
		**Note:**
		The colab notebook has MAX_LEN = 100 by default, and the bert model is trained using this input dimensions. This is also reflected in `backend/config.py`.
		However, if you want to change the MAX_LEN value:

	 - Change the MAX_LEN value in `backend/config.py`.
	 - Change the MAX_LEN value in the python notebook.
	 - Rerun the python notebook to obtain new model weights which take has input dimesnsions set to new MAX_LEN value
	 - Download and save the model weights in `backend/models/`
	 - Update the `backend/config.py` variables for MODEL_PATH and MODEL_NAME as required


 - The above code is run using `docker` and `docker-compose`. To start the application using `docker-compose`, simply run:


	    docker-compose up -d --build

	This will build the docker images, and automatically start the following:
	- FastAPI server on port 8000
	- Streamlit front end on port 8501
- To run the backend and frontend files without docker
	- backend:


		    cd backend/
		    pip install -r requirements.txt
		    python main.py

	- frontend:
		Before running the file, you need to edit `frontend/main.py`, replace the url `http://backend:8000/predict` by `http://0.0.0.0:8000/predict`. Then run the following:


		    cd frontend/
		    pip install -r requirements.txt
		    streamlit run main.py
	**Note:** The fastapi server usually takes some time to start the first time as it needs to download `bert` and its `tokenizer` from `tensorflow-hub`. Once downloaded it should be cached.

### About the dataset
A dataset for sexually harassing text was not readily available online. Hence our team built a new dataset by scraping the tweets from Twitter. The dataset is available in the accompanying project repository [here](https://github.com/whopriyam/Sexual-Harassment-Classification/blob/main/Labelled_Tweets/Cleaned_tweets.csv).
The summary of the scraped dataset containing sexually harassing words is provided below:
| **Word**  | **Positive Samples** | **Negative Samples** | **Word** | **Positive Samples** | **Negative Samples** |
|------------------|-------------------------------|-------------------------------|-------------------|-------------------------------|-------------------------------|
| anal             | 2                             | 0                             | cunnilingus       | 21                            | 5                             |
| aroused          | 414                           | 133                           | cunt              | 29                            | 100                           |
| ass              | 89                            | 155                           | cunt rag          | 1                             | 7                             |
| ass cowboy       | 17                            | 55                            | cuntass           | 8                             | 37                            |
| assbandit        | 1                             | 27                            | cuntfuck          | 2                             | 2                             |
| assblaster       | 5                             | 11                            | cunthole          | 5                             | 10                            |
| assclown         | 9                             | 11                            | cuntlick          | 3                             | 0                             |
| assfucker        | 4                             | 5                             | cuntlicker        | 1                             | 0                             |
| asslick          | 11                            | 0                             | dick beaters      | 4                             | 14                            |
| asslicker        | 13                            | 0                             | dick for brains   | 19                            | 37                            |
| assMan           | 5                             | 0                             | dick licker       | 4                             | 11                            |
| bad fuck         | 58                            | 115                           | dickslap          | 3                             | 0                             |
| ball licker      | 5                             | 19                            | dicksucker        | 1                             | 0                             |
| balls            | 91                            | 126                           | dyke              | 3                             | 7                             |
| bastard          | 2                             | 52                            | eat me            | 4                             | 21                            |
| big butt         | 65                            | 64                            | eat pussy         | 228                           | 0                             |
| bitch            | 27                            | 121                           | ejaculate         | 12                            | 1                             |
| bitch ass        | 13                            | 33                            | erection          | 7                             | 7                             |
| bitchtits        | 16                            | 29                            | faggot            | 1                             | 1                             |
| bite me          | 33                            | 30                            | finger fuck       | 3                             | 1                             |
| blowjob          | 3                             | 2                             | finger fucker     | 1                             | 0                             |
| blowjob          | 5                             | 0                             | fingerfucking     | 13                            | 0                             |
| boobies          | 100                           | 69                            | fist fuck         | 1                             | 1                             |
| boobjob          | 3                             | 3                             | prostitute        | 27                            | 14                            |
| boobs            | 28                            | 27                            | pussy             | 4                             | 0                             |
| breast job       | 1                             | 24                            | puss              | 12                            | 1                             |
| breast man       | 9                             | 28                            | pussie            | 14                            | 2                             |
| brothel          | 3                             | 8                             | pussies           | 1                             | 2                             |
| bumblefuck       | 2                             | 0                             | pusy              | 8                             | 0                             |
| butt             | 25                            | 22                            | rapist            | 5                             | 4                             |
| butt pirate      | 2                             | 0                             | schlong           | 13                            | 2                             |
| buttfuck         | 5                             | 3                             | semen             | 8                             | 4                             |
| carpet   muncher | 2                             | 1                             | skank bitch       | 39                            | 8                             |
| chode            | 25                            | 7                             | skank fuck        | 13                            | 6                             |
| clit             | 39                            | 4                             | skank whore       | 5                             | 1                             |
| cock             | 6                             | 4                             | skanky            | 7                             | 7                             |
| cock block       | 5                             | 5                             | slut              | 85                            | 9                             |
| cock smoke       | 11                            | 2                             | sluts             | 35                            | 15                            |
| cock suck        | 29                            | 0                             | slutt             | 1                             | 1                             |
| cockhead         | 4                             | 5                             | slutwhore         | 2                             | 0                             |
| cocksucking      | 1                             | 0                             | sodomize          | 8                             | 2                             |
| coochie          | 24                            | 5                             | suck              | 21                            | 13                            |
| cum              | 9                             | 1                             | tittie            | 9                             | 4                             |
| cum bubble       | 3                             | 0                             | wanking           | 3                             | 7                             |
| cum guzzler      | 2                             | 1                             | whore             | 32                            | 12                            |
| cumming          | 14                            | 2                             | whorefucker       | 1                             | 0                             |
| cunilingus       | 6                             | 5                             |                   |                               |                               |
