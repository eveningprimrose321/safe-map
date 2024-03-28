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


## 如何使用 Safe Map 網頁平臺 
先進入`safemap-webpage`資料夾，在裡面會有`frontend`及`backend`兩個資料夾，分別存放前端及後端所需的檔案。  

文件說明請見`frontend`及`backend`資料夾之README或點擊[frontend](https://github.com/Wilson330/Safe_Map/)和[backend](https://github.com/Wilson330/Safe_Map/)。

### 1. Frontend 設定
為了存取Google Map的地圖資訊，請先至Google Cloud Platform申請API key，此動作需要先新開專案，到**API及服務**欄位選取**憑證**並建立**API金鑰**，再將**Maps JavaScript API**啟用即可。(詳細步驟可以搜尋"google api key申請")  

之前這個API是有每月的額度上限，但現在改為90天的免費計畫，所以我的已經過期了QQ，有興趣可至Google Cloud Platform查看。(Note: 要綁定信用卡才能用喔！)  

#### #操作步驟
建立**Node.js開發環境**並設置**npm** (記得安裝LTS版本比較穩定！)，要注意node.js和npm都有加入環境變數中。  

開啟cmd並切換至`frontend`資料夾，並輸入以下指令以安裝package.json中所有dependencies。  

    npm install

於資料夾中建立檔案`.env.local`，並於內部輸入以下內容，其中`key`的部分要修改為前面步驟取得的**Google API key**。

    REACT_APP_GOOGLE_MAPS_API_KEY = key

如此便完成Frontend設定！

### 2. Backend 設定
#### #操作步驟
建立osmnx之Python環境 (使用conda)

    conda config --prepend channels conda-forge 
    conda create -n ox --strict-channel-priority osmnx

此為官方支援的安裝方式，詳細可見[此頁面](https://osmnx.readthedocs.io/en/stable/installation.html)。(**Note:** 也可以使用`pip install osmnx`來進行安裝，但可能會缺少部分套件。)  

切換至ox環境後，安裝所需套件

    pip install -r requirements.txt

如此便完成Backend設定！  

### 3. 執行
#### #Frontend
切換至`frontend`資料夾，於使用npm啟動app

    npm start

#### #Backend
切換至`backend`資料夾，並調整至ox環境，於本機啟動伺服器

    python app.py runserver

即可開始使用！

### 4. 使用
請輸入**起點**及**終點**之地點名稱，並於右側滑動條調整**安全係數**的大小，越大表示安全性的權重越高，最後點擊**Calculate Route按鈕**即可獲得路徑。  

#### 實際使用頁面如下圖：
![Webpage](img.PNG "safeRoute")

**Credit:**  
前端網頁設計及React架構參考自：**trulymittal** 大神的 [google-maps-directions-tutorial](https://github.com/trulymittal/google-maps-directions-tutorial/tree/master)  

清大人工智慧課程期末專題  
組員：工科系碩士班 **李松鴻、許維珅、林子芸、朱惠瑜**
