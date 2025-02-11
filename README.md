AIT614-001
Team 1
Readme file
Operating system: Windows 11 Home
Setting up WSL:
1.	Open the command prompt of the windows machine as an administrator to avoid the permission issues.
2.	Use the command “apt install wsl” to install the windows subsystem for linux (ubuntu).
 ![image](https://github.com/user-attachments/assets/0fcd48da-47f1-454d-832f-37c81d89b073)

3.	Close the command prompt once ubuntu is installed.
4.	Ubuntu will be visible in the start menu.
Setting up docker and MongoDB:
1.	Launch the ubuntu application.
2.	Shift to the root user using the command “sudo su”
3.	Use the command “apt install docker.io” to install docker
 ![image](https://github.com/user-attachments/assets/7e5c2b5d-eaa8-4157-9516-47c5e95aa71a)

4.	Enable the docker using the commands “sudo systemctl start docker” and “sudo systemctl enable docker”
 
![image](https://github.com/user-attachments/assets/3efbccbf-2778-42a0-b501-d0a432fd2b0a)



5.	Use the command “docker pull mongo” to install the MongoDB container
 ![image](https://github.com/user-attachments/assets/6ab07987-f137-417f-985f-fc4786fbc42d)

6.	To run the MongoDB container, we use the command “docker run -d --name my-mongo-container -p 27017:27017 -v /root/AIT614:/data mongo --bind_ip 0.0.0.0”
Here, “my-mongo-container” is the name of the container, “27017” is the MongoDB port and “ /root/AIT614” is the location of the folder where the dataset is located. “--bind_ip 0.0.0.0” is used to allow traffic from and to the container
 ![image](https://github.com/user-attachments/assets/2e7bccf2-bc76-4c19-8b6c-d7ad7ed93e8f)

7.	Import the data into MongoDB using the command “docker exec -i my-mongo-container mongoimport --db my_database --collection my_collection --type csv --file /data/telecom_churn.csv --headerline”. In this command, “mongoimport” is the function used to import the data, “my_database” is the database name, “my_collection” is the collection name, since the data in MongoDB is saved as documents in a collection. We have mentioned the the file path as “/data/telecom_churn.csv”.
 ![image](https://github.com/user-attachments/assets/39fab56d-a749-4644-b926-e6ac90a2b840)

Setting up Ngrok:
1.	To use Ngrok, we need to set up a free account and update credit card  information to gain access(There is no charge up to 1GB transfers). We need to use the command provided in ngrok along with the token to enable Ngrok.
 ![image](https://github.com/user-attachments/assets/be30b336-838d-491f-b654-c3181875e889)

2.	Use the command “ngrok tcp 27017” to get the url that will enable the connection between MongoDB and Databricks. 
 ![image](https://github.com/user-attachments/assets/36b860ed-b8f4-400d-866f-ab1ad7fc7836)

Running the ipynb file:
Upload the ipynb file to Databricks.
Create a cluster and connect it to the ipynb notebook.
Cell 3: This cell holds the url for MongoDB which is the url provided by Ngrok
 ![image](https://github.com/user-attachments/assets/5b530636-8f46-4749-973f-d1c71fdb560f)

The rest of the cells can be run.
Note: Since the SVM cells take more time and there is a limit on the cluster, cells 1-11,17,21 need to be run multiple times with a new cluster each time to run each SVM with a different kernel.
