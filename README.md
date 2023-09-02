# Travel Memory

`.env` file to work with the backend:

```
MONGO_URI='ENTER_YOUR_URL'
PORT=3000
```

Data format to be added: 

```json
{
    "tripName": "Incredible India",
    "startDateOfJourney": "19-03-2022",
    "endDateOfJourney": "27-03-2022",
    "nameOfHotels":"Hotel Namaste, Backpackers Club",
    "placesVisited":"Delhi, Kolkata, Chennai, Mumbai",
    "totalCost": 800000,
    "tripType": "leisure",
    "experience": "Lorem Ipsum, Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum, ",
    "image": "https://t3.ftcdn.net/jpg/03/04/85/26/360_F_304852693_nSOn9KvUgafgvZ6wM0CNaULYUa7xXBkA.jpg",
    "shortDescription":"India is a wonderful country with rich culture and good people.",
    "featured": true
}
```
Steps to Deploy an application and establish a connection between Frontend, Backend, and the database.

Configuring Mongo DB

1. Need to open the cloud Mongo DB website and create a new cluster. For a free account, we have the option to create one free cluster.
2. To create a cluster, we need to click on Create and select Shared, then select Cluster Details add the name of the cluster, and click on Create a cluster.
3. Click on the cluster name and click on Connect. A tab will open, Click on compass, and select I have MongoDB compass installed, Copy the connection string link and paste the same link in the backend that is in the .env file.

Creating an Instance and configuring a database
1. Create 2 instances with the same VPC, while creating an instance, we must select 2 instances so that the same security group will apply to both instances.
2. Open the MongoDB website in the browser and create a new cluster named travelmemory.
3. We have created a username and password for the connection part.
4. Keep the copied db link and use this in the frontend application.

Configuring Frontend

1. We need to open the EC2 instance and clone the Git repo (sudo git clone https://github.com/UnpredictablePrashant/TravelMemory.git) where the code is placed.
2. We will go to the repo and open cd TravelMemory/
3. Install node js v18 which is the stable version by this command
    curl -s https://deb.nodesource.com/setup_18.x | sudo bash
    sudo apt install nodejs -y
    node -v  # to check the version of node js
5. Then you will install all the dependencies using the below command
    npm install
6. After that, we need to open ls and you will find package.json and perform the below command
    sudo nano package.json
7. After that find start and insert the below content
   scripts": {
    "start": "PORT=80 react-scripts start",
8. Now we have configured everything in the front end and are good to go.
    sudo npm start --port 80
5. Need to create .env file in the backend and edit the url with frontend ip:80    

Configuring backend

1. We need to clone the repo as mentioned above
2. We need to go to the folder
     cd /home/ubuntu/TravelMemory/
3. We need to create a .env file using the below command and need to put the database link to establish a connection between the backend and the database
    sudo nano .env
    MONGO_URI = "mongodb+srv://<username>:<password>@travelmemory.h5dvcda.mongodb.net/"
    PORT = 80
4. After that we need to run the below command to run the index.js file
    node index.js -p 80

    

To check whether the application is working or not

1. Once this is done, we need to run the below command in the frontend server/instance
    sudo npm start --port 80
2. After that, we need to copy the IP address of the frontend server/instance and place the port no 80. Below is the command.
        frontendIP:80
