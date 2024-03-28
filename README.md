# Safe Map: Secure Path Planning Integrating Streetlight and Surveillance Camera Data

## Abstract
 When requesting navigation directions, Google Map provided routes based solely on the shortest distance. The routes with shortest distance sometimes considered dimly lit alleys which might be lack of enough streetlights and surveillance cameras, and this may results in a safety considerations.
 
 To address this issue, we have employed route planning algorithms to identify safer routes, taking into account the density of streetlights and surveillance cameras along the way.

 Implementing area: Taiwan, Hsinchu City (The location of National Tsing Hua University!)


## Data Resources

### Dataset of Streetlight and Surveillence camera:
政府資料開放平臺：[新竹市錄影監視系統設置地點](https://data.gov.tw/dataset/67490)  
新竹市政府資料開放平臺：[新竹市公有道路路燈資料](https://opendata.hccg.gov.tw/OpenDataDetail.aspx?n=1&s=159)  

### Street Map Data:
Python package of OpenStreetMap：[OSMnx](https://osmnx.readthedocs.io/en/stable/)  
Google Map API：[GoogleCloudPlatform](https://console.cloud.google.com/)  

## Data Preprocessing and Analysis
First, we combined the location information from the streetlight and surveillance camera datasets with OpenStreetMap (OSM) data, utilizing the longitude and latitude of each streetlight/surveillance camera.

We employed Kernel Density Estimation to analyze the density of streetlight/surveillance camera in each area. Each node in the OSM graph received a score based on the density of streetlight/surveillance camera surrounding it. This score could influence the outcome of the route optimization algorithms, depending on the security factor chosen by the user.

We tested two different route optimization algorithms (A* Algorithm and Dijkstra's Algorithm) and compared their performances. Dijkstra's Algorithm was chosen for the final web version due to its higher computational speed.


## How to use Safe Map

In the `safemap-webpage` folder are the `frontend` and `backend` folders. All the needed files are in these folders.

The `frontend` structure is refered to **trulymittal** [google-maps-directions-tutorial](https://github.com/trulymittal/google-maps-directions-tutorial/tree/master).

### 1. Frontend Settings
#### Step 1
Create an API in the [google developers console](https://console.developers.google.com), make sure to enable billing for the google project. (You can find how to do this by searching "get google api key")  

#### Step 2
Build a **Node.js Environment** with installing **Node.js** and **npm**. Make sure that both `Node.js` and `npm` are added in the system environment path.

To install all the packages used in this project, open cmd and cd to `frontend` folder, enter the following command to install all the packages listed in `package.json` and their dependencies:

    npm install
    
Or you can also use `yarn`:

    yarn install

#### Step 3
Add a .env file or .env.local in the `frontend` folder and add the following content (edit it as a text file) to specify your API key:

    REACT_APP_GOOGLE_MAPS_API_KEY=your_api_key_here
    

### 2. Backend Settings
Install [osmnx](https://osmnx.readthedocs.io/en/stable/installation.html) and [flask](https://flask.palletsprojects.com/en/3.0.x/installation/)in your python environment.


### 3. RUN!!!
#### #Frontend
cd to `frontend` folder and run:

    npm start
    
(or run

    yarn start

if you use yarn in the previous step)

#### #Backend
cd to `backend` folder (make sure you have activated the correct environment!) and run:

    python app.py runserver

TA-DA!


#### #**A (slightly) easier way to run**

Open `start.txt`, and change the second line `conda activate AI` to 

    conda activate YOUR_ENV_NAME

 and rename the file extension `.txt` to `.bat`.

You can just double click the `start.bat` to run this project.
(But make sure all the package installations and the API key setting have been done well!)



**Credit:**  
The whole `frontend` structure is refered to **trulymittal** [google-maps-directions-tutorial](https://github.com/trulymittal/google-maps-directions-tutorial/tree/master)  

國立清華大學人工智慧課程期末專題  
組員：工科系碩士班 **李松鴻、許維珅、林子芸、朱惠瑜** (Special thanks to **詹凱錞**)
