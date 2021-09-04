# binance-trading-robot
The objective of this project is to create a cryptocurrency buying and selling robot to operate from signals sent by TradingView.com indicators

## Description
This is the same [@amfchef](https://github.com/amfchef) binance-trading-robot running on Firebase and Cloud Run hosting a Flask server using Docker.
I followed this [video](https://www.youtube.com/watch?v=t5EfITuFD9w) and migrated amfchef's [code](https://github.com/amfchef/binance-trading-bot) to run on [Firebase](https://firebase.google.com/) 

## Getting Started
### Dependencies
#### Check what you have
* check you JAVA version on Terminal or CMD
```bash
java -version
```
* check you PYTHON version on Terminal or CMD
```bash
python3 --version
```
* check you NODE version on Terminal or CMD
```bash
node --version
```
* check you NPM version on Terminal or CMD
```bash
npm --version
````
* install whatever package above you don't have. I'm using: 
  * PYTHON: 
    * 3.8.2 
  * JAVA:
    * 16.0.2
  * NODE:
    * 10.24.1  
  * NPM:
    * 7.21.1 

#### Install a text editor or IDE
The guy on the video is using https://code.visualstudio.com/ (this was recommended in the video above, I'm using it as well)
#### Install Google Cloud SDK
you can find how to do that here https://cloud.google.com/sdk/docs/quickstart
#### login to gcloud
```bash
gcloud auth login
```
#### initialize gcloud
```bash
gcloud init
```

* Pick configuration to use:
   * Create a new configuration

* Choose the account you would like to use to perform operations for 
this configuration:
   * select your email

* Pick cloud project to use: 
   * create a new project

* Enter a Project ID
   * give it a name


#### Enable project billing and Cloud APIs 
you can find it searching for the API name on https://console.cloud.google.com/
* Enable Cloud Run API
* Enable Cloud Build API
* Enable Secret Manager API

#### API Key and password setup
Go to https://console.cloud.google.com/ and search for Secret Manager
* create key, secret on Binance (remember to allow margin)

* create key, secret and password on Google Secret Manager

* add the security rule Secret Manager Accessor for yor blablabla.compute@developer.gserviceaccount.com

### Installing
#### Clone my bundle
Clone my code bundle at https://github.com/danielvm-git/binance-trading-robot and put in your project folder
```bash
git clone https://github.com/danielvm-git/binance-trading-robot
```

#### Put your keys
Open the source code folder with VSCode and edit the files to put your keys on

* 1st here: /server/src/calculate.py (you find this adding an app on your Firebase console -> Project Overview -> Settings -> General)
     * change project_id (here is the name)
     * change key_request ("projects/<put your project number here>/secrets/exchange_api_key_binance_margin/versions/latest")
     * change secret_request ("projects/<put your project number here>/secrets/exchange_api_secret_binance_margin/versions/latest") 

* 2nd here: /server/src/serviceAccountKey.json (you find this creating a Service account on your Firebase console -> Project Overview -> Settings -> Service Account)
 
#### create de build
Open a Terminal inside your VSCode.
If it's not on you projec folder you first go to the folder where you cloned the repository

```bash
cd .../binance-trading-robot
````
go to your server folder
```bash
cd server
```
And than, inside the folder you execute this command
```bash
gcloud builds submit --tag gcr.io/<put the name of your Google Cloud PROJECT here>/<put the name of your Cloud Run FUNCTION here>
```
#### deploy new build
```bash
gcloud run deploy --image gcr.io/<put the name of your Google Cloud PROJECT here>/<put the name of your Cloud Run FUNCTION here>
```
#### Create firebase project binance-trading-robot
go to https://firebase.google.com/ and create a new project to host the role thing

Then go back to your project main folder

```bash
cd ..
```
And than, inside the folder you execute this command
```bash
npm init
```
and then this
```bash
npm i -D firebase-tools
```

#### init firebase hosting
use this command:
```bash
firebase init hosting
```
That's it!
Go to the https://console.cloud.google.com/ -> Cloud Run and the adress of the service is your webhook. Just use it on your TradingView with MM and this strings on the message of the alert:
 https://github.com/danielvm-git/binance-trading-robot/blob/main/server/src/Webhook/Webhook%20samples.txt

## Help
### What I did to get here 
Those where my notes during the process, it's a mess but maybe can help you
### Followed the video
I Followed the video and built the application like you see on the video https://www.youtube.com/watch?v=t5EfITuFD9w
The idea is to run @amfchef's code on this structure instead of the presenter's one. 
#### Downloaded the original code
Cloned @amfchef bot at https://github.com/amfchef/binance-trading-bot Great job guy, the code is amazing
#### Moved the files
Moved original files and replace the ones on my the application I built watching the video. Created the function binance-trading-robot-fire on Cloud Run
#### Created the Docker
Created docker file like you see on the video then you add this to the RUN line:  
python-binance binance Werkzeug google-cloud google-cloud-bigquery google-cloud-secret-manager firebase-admin pandas pyarrow
#### Put my keys
Edited the config files and put my keys on

1st here: /server/src/serviceAccountKey.json (you find this adding an app on your Firebase console -> Project Overview -> Settings -> General)

2nd here: /server/src/config.py (you find this creating a Service account on your Firebase console -> Project Overview -> Settings -> Service Account)

#### created de build
```bash
gcloud builds submit --tag gcr.io/binance-trading-robot/binance-trading-robot-fire
```
#### deployed new build
```bash
gcloud run deploy --image gcr.io/binance-trading-robot/binance-trading-robot-fire
```
#### Created firebase project binance-trading-robot
went to https://firebase.google.com/ and create a new project to host the role thing
#### init firebase hosting
used this command:
```bash
firebase init hosting
```

## Authors

[@amfchef](https://github.com/amfchef) 
[@danielvm-git](https://github.com/danielvm-git)

## Version History

* 0.1
    * Initial Release

## License

This project is licensed under the MIT License - see the LICENSE.md file for details

## Acknowledgments

