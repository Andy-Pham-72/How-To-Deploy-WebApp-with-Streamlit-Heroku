# :computer: How To Deploy A Simple WebApp with Streamlit Heroku :computer:

This was one of my mini lectures when I created for the students to have a quick and intuitive tutorial of how to create a simple webapp with Streamlit and Heroku.

I also have a notebook to lead the beginner through step by step very detailed and straightforward via this: [link](https://github.com/Andy-Pham-72/How_To_Deploy_WebApp_with_Streamlit_Heroku/blob/master/Steps%20to%20deploy%20your%20Webapp%20with%20Streamlit%20on%20Heroku/Deploy%20WebApp%20with%20Streamlit%20on%20Heroku.ipynb)

I encourage people take a look at the Streamlit [documentation](https://docs.streamlit.io/en/stable/api.html) before creating our own WebApp.

You can check my simple WebApp with this [link](https://andy-cool-webapp.herokuapp.com/).

# Create a Web App with Streamlit and deploy on Heroku
### (with the pre-made webapp.py)

### 1. Installation
Open Terminal/ Git Bash and run:
```bash
$ pip install streamlit
```

### 2. Create a working directory

- Unzip the file to the directory of your choice.
- The heart of the web app is `webapp.py` file which you can find all the codes.

### 3. Deploy the web app locally
Open Terminal/ Git Bash, using `cd` command to the directory where you unzip the file and run this command below:
```bash
$ streamlit run webapp.py
```
- Another browser tab will popup and show you the web app or you can copy and paste the `Local URL` which is generated by Streamlit to your browser. For example, from the terminal you can see:

```bash
  You can now view your Streamlit app in your browser.

  Local URL: http://localhost:8502   
```
![image](https://drive.google.com/uc?export=view&id=1_HMrwevnDAX-J7nXfCEMATNIygdW2WZ5)


### 4. Deploy the web app on Heroku
- Now you want other people could have the access to your awesome web app which is made easy with Heroku!

#### 4.1 Create necessary files for Heroku
- Along with the `webapp.py` and the `data` folder that you need for Streamlit web app, we have to create some **necessary files** in order to deploy it on Heroku:

   
1. `requirements.txt` : will tell Heroku to install the following Python library and the corresponding version as the screenshot below:

   
   ![Screen Shot 2021-05-05 at 9.14.58 PM.png](attachment:a62a26bf-1343-4213-ad86-cea75e9bd090.png)
     
  **NOTE**: You may don't want to find these information manually so there is a Python library called `pipreqs` that can find all the library version that you're use for the webapp.py. Go to your Terminal/ Git Bash and run these command:

```bash
$ pip install pipreqs

 using cd command to your directory of the web app folder and run command:
 
$ pipreqs ./
```

=> It will produce `requirements.txt` file that contains the needed Python libraries! 
     
  **BUT WAIT!!!** There is one library that `pipreqs` didn't catch which is the `scikit-learn` library since it's not explicitly mentioned in the webapp.py. Because we are using `sentiment_pipeline.pkl` file, which was dumped by joblib, to predict the sentiment of a sentence and it was built by the `scikit-learn` library. Easy! We just need to run this command in Terminal/ Git Bash:
<br>

```bash
$ conda list
```

=> You can find the right `scikit-learn` version which is `0.23.2` to add to the `requirements.txt` file:

![Screen Shot 2021-05-05 at 9.52.58 PM.png](attachment:3d4c4dec-b4bd-4b09-90da-c965aa9a09e0.png)


2. `setup.sh` : will handle issues regarding the server side in terms of the port number & it will add it to the configuration. You can just copy this .sh file to your folder, **it doesn't need to be changed**.
<br>

     ![Screen Shot 2021-05-05 at 9.18.51 PM.png](attachment:e605fcef-2849-4f40-960a-abb962006ebc.png)
     
3. `Procfile` : Essentially runs the `setup.sh` file and run the `webapp.py`. You can just copy the code in this file and only change the name of the `.py` file of your choice when you creat a web app (in our case is `webapp.py` ). 
     
   **NOTE**: `Procfile` **doesn't have any extension** so you just need to save it as `Procfile`.
   <br>
   
   ![Screen Shot 2021-05-05 at 9.21.42 PM.png](attachment:b6bcc3b4-11ed-40cc-9384-15d7777fb478.png)
   
#### 4.2 Upload your folder to your Github repository.
- Create a new repository with any name of your choice and make sure it's `Public` :

![Screen Shot 2021-05-05 at 10.03.14 PM.png](attachment:ffb5c613-b352-4dd8-b222-e868439627d4.png)

- Go to Terminal/ Git Bash and use `cd` command to navigate to the web app folder directory then run these commands to upload to your repository:

```bash
$ git init
$ git add .
$ git commit -m "first commit"
```

Now you have to go to your github to copy this link in your git repository as screenshot below (this step only takes one time to do):

![Screen Shot 2021-05-05 at 10.12.42 PM.png](attachment:4ca4cbdd-bddf-4d25-b4bc-3a4c26dc792e.png)

back to your Terminal/ Git Bash and run these commands (please replace below GitHub repository link to your repository link):

```bash
$ git remote add origin https://github.com/andypham0702/web-app.git
$ git push -u origin master
```

You may have to input your github username and password in order to upload all the fils to your git repository. <br>
Awesome! Now all the files are uploaded to your git repository!

![Screen Shot 2021-05-05 at 10.34.05 PM.png](attachment:383c8fed-5512-4178-bbac-ea28acc561a2.png)


#### 4.3 Deploy web app on Heroku.

- Create an account in `https://www.heroku.com/` 
- Create an unique name for your web app:

![Screen Shot 2021-05-05 at 10.52.40 PM.png](attachment:47c5f9c6-e8b1-4901-bbb0-3a067e0ad32a.png)

- In the `Deployment method` choose `GitHub` and connect to your repository as screenshot below:

![Screen Shot 2021-05-05 at 10.54.06 PM.png](attachment:83876bdd-a0e4-4f9f-9c40-abab568247ec.png)

- Scroll down and click `Deploy Branch` :

![Screen Shot 2021-05-05 at 10.56.25 PM.png](attachment:568dc5c2-7316-49f5-b8b2-acdf4b7f9117.png)

Great! After it's successfully deployed, now you can access the web app with this link: https://andy-cool-webapp.herokuapp.com

**NOTE:** if the you fail to deploy the webapp, it means you have to check `requirements.txt` and `Procfile` that they contains appropriate information.

**EXTRA material:**

- Since Streamlit can show Emoji so you can find a list of supported emojis in this link: https://www.webfx.com/tools/emoji-cheat-sheet/

- How `st.cache` can help to improve the web app performance: https://docs.streamlit.io/en/stable/caching.html

- For all your Streamlit questions, check out their documentation: https://docs.streamlit.io/en/stable/api.html
