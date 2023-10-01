## Table of Contents

1. [Creating Instances](#creating-instances)
2. [Configuring Backend](#configuring-backend)
   1. [Creating env File](#creating-env-file)
   2. [Installing Nginx Reverse Proxy](#installing-nginx-reverse-proxy)
   3. [Setting Up Reverse Proxy](#setting-up-reverse-proxy)
   4. [Enabling Nginx Configuration](#enabling-nginx-configuration)
   5. [Restarting Nginx](#restarting-nginx)
3. [Configuring Frontend](#configuring-frontend)
   1. [Installing Dependencies](#installing-dependencies)
   2. [Cloning the Repo](#cloning-the-repo)
   3. [Installing Dependencies](#installing-dependencies-1)
   4. [Editing package.json File](#editing-packagejson-file)
   5. [Starting the Server](#starting-the-server)
   6. [Reverse Proxy for Frontend Server](#reverse-proxy-for-frontend-server)
4. [Scaling the Application Using Load Balancer](#scaling-the-application-using-load-balancer)
   1. [Creating an Image](#creating-an-image)
   2. [Launching an Instance from the Image](#launching-an-instance-from-the-image)
   3. [Launching the Instance Using AMI](#launching-the-instance-using-ami)
   4. [Performing the Same Tasks for the Backend](#performing-the-same-tasks-for-the-backend)
   5. [Checking the Visibility of TravelMemory](#checking-the-visibility-of-travelmemory)
5. [Configuring Target Groups and Load Balancer](#configuring-target-groups-and-load-balancer)
   1. [Creating Target Groups](#creating-target-groups)
   2. [Selecting Frontend Instances](#selecting-frontend-instances)
   3. [Including as Pending](#including-as-pending)
   4. [Creating Target Group](#creating-target-group)
   5. [Configuring Load Balancer Using Instances](#configuring-load-balancer-using-instances)
   6. [Performing the Same Process for the Backend](#performing-the-same-process-for-the-backend)
6. [Configuring Load Balancer](#configuring-load-balancer)
   1. [Selecting Application Load Balancer](#selecting-application-load-balancer)
   2. [Choosing at Least 2 Availability Zones](#choosing-at-least-2-availability-zones)
   3. [Keeping Default Configuration](#keeping-default-configuration)
   4. [Creating Load Balancer](#creating-load-balancer)
   5. [Taking Load Balancer DNS and Configuring in Cloudflare](#taking-load-balancer-dns-and-configuring-in-cloudflare)
7. [Testing the Load Balancer Configuration](#testing-the-load-balancer-configuration)
   1. [Changing Backend URL in url.js](#changing-backend-url-in-urljs)

Citations:
[1] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/2184209/af62280e-70c6-45d0-bf61-666b65578b3f/MERNProject_35983144.pdf

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

## Configuring Mongo DB

1. Need to open the cloud Mongo DB website and create a new cluster. For a free account, we have the option to create one free cluster.
2. To create a cluster, we need to click on Create and select Shared, then select Cluster Details add the name of the cluster, and click on Create a cluster.
3. Click on the cluster name and click on Connect. A tab will open, Click on compass, and select I have MongoDB compass installed, Copy the connection string link and paste the same link in the backend that is in the .env file as shown in the backend configuration.

## Creating an Instance and configuring a database
1. Create 2 instances with the same VPC, while creating an instance, we must select 2 instances so that the same security group will apply to both instances.
2. Open the MongoDB website in the browser and create a new cluster named travelmemory.
3. We have created a username and password for the connection part.
4. Keep the copied db link and use this in the frontend application.

## Configuring Frontend

1. We need to open the EC2 instance and clone the Git repo
```
sudo git clone https://github.com/UnpredictablePrashant/TravelMemory.git
```
![image](https://github.com/sayanalokesh/TravelMemory/assets/105637305/f2d2884f-4f1e-4c4b-8acb-05c53039cccf)

2. We will go to the repo and open cd TravelMemory/


4. Install node js v18 which is the stable version by this command
    ```
   curl -s https://deb.nodesource.com/setup_18.x | sudo bash

    ```
   ![image](https://github.com/sayanalokesh/TravelMemory/assets/105637305/54dcea2c-5cbd-4c29-8937-3ed1f1de2b9b)
   
    ```
    sudo apt install nodejs -y
    ```
   
   ![image](https://github.com/sayanalokesh/TravelMemory/assets/105637305/afe88175-e428-4f70-8e81-98bccbb5093f)
   
    ```
    node -v  # to check the version of node js
    ```
   
   ![image](https://github.com/sayanalokesh/TravelMemory/assets/105637305/a8cafd5f-3a18-45c3-a9f4-b6277c5207b4)

   
5. Then you will install all the dependencies using the below command
    ```
    npm install
    ```
   
   ![image](https://github.com/sayanalokesh/TravelMemory/assets/105637305/814eeb07-8854-4f70-a090-e627e3740c29)


8. After that, we need to open ls and you will find package.json and perform the below command
    ```
    sudo nano package.json
    ```
9. After that find start and insert the below content
   ```
   scripts": {
    "start": "PORT=80 react-scripts start",
   ```
10. Now we have configured everything in the front end and are good to go.
    ```
    sudo npm start --port 80
    ```
11. Need to create url.js file in the backend and edit the url with backend ip:80
   ```
    export const baseUrl = "<backendIP>:80"
   ```

## Configuring backend

1. We need to clone the repo as mentioned above
2. We need to go to the folder
3. ```
     cd /home/ubuntu/TravelMemory/
   ```
4. We need to create a .env file using the below command and need to put the database link to establish a connection between the backend and the database

   ```
    sudo nano .env
    MONGO_URI="mongodb+srv://<username>:<password>@travelmemory.h5dvcda.mongodb.net/travelmemory"
    PORT=3000
    ```
   
    ![image](https://github.com/sayanalokesh/TravelMemory/assets/105637305/1802a020-0c3b-4a2c-9042-f0c3130de92a)

6. After that we need to run the below command to run the index.js file
    ```
    node index.js
    ```

## Configuring the backend with the Domain Name using Cloudflare

1. We need to purchase a domain name from Godaddy.
2. We need to log in to [Cloudflare](https://dash.cloudflare.com/) and add our domain by clicking on addsite.
3. Once we add the domain name, we can see the name servers. We need to copy the name servers and add the same to the Godaddy website under our domain/DNS/Nameservers.
4. Again go to Cloudflare - DNS - Records.
5. Click on add records - select type as A, and enter our domain name lokeshsayana.co.in under Name and give the IP address of the backend server in the IPv4 address
6. ![image](https://github.com/sayanalokesh/TravelMemory/assets/105637305/cac9346e-df9a-4ede-91aa-dc56687e1c7f)

## Reverse Proxy

1. Earlier we ran the application inport 80. We will now change the port to 3000 and run the Nginx server on port 80.
2. For that we need to make changes in .env file as below.
3. ![image](https://github.com/sayanalokesh/TravelMemory/assets/105637305/cf8fa60d-6776-40b5-bb63-585b2bcc4e9c)
4. 



## To check whether the application is working or not

1. Once this is done, we need to run the below command in the frontend server/instance
    sudo npm start --port 80
2. After that, we need to copy the IP address of the frontend server/instance and place the port no 80. Below is the command.
        frontendIP:80

