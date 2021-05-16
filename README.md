# Door Access Control System API
<div align="center">
  <img src="https://user-images.githubusercontent.com/74485621/113541799-e67b7280-961d-11eb-87b1-7dd5f4bef890.png"><br>
</div>

-----------------
## What is it?
**Door Access Control System API** is an api for a report on door access.<br>
Built and deployed through **Elastic Beanstalk of AWS**.
## Project Structure
```
├── .ebextensions
│   └── django.config
├── accesses
├── accounts
├── door_access_control_system
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── .gitignore
├── README.md
├── manage.py
└── requirements.txt
```
* `django.config/.ebextensons` : File that configure the environment and customize the AWS resources that it contains when the server is deployed 
* `accesses`: Include API function code related to entrance report details
	* `DoorUseLogList` : The functions to look up the full list of entrance to the door. Using generics and permission(IsAdminUser) in DRF
	* `DoorUseLogDetailList` : The functions to inquire the detailed list by door entry and exit generation. Using APIView and custom permission(IsAdminOrGeneration) in DRF
	* `GenerationAdminList` : Full list of administrator entry and exit functions with costs. Using APIView and permission(IsAdminUser) in DRF
	* `GenerationPublicList` : Detail list of generations entry and exit functions with costs. Using APIView and custom permission(IsAdminOrGeneration) in DRF
	* `ApiList` : Include endpoint list
* `accounts` : Include API feature code related to the user
    * `CreateUser` : The function to create user. Using custom model(UserManager) and generics in DRF
* `requirements.txt` : Define libraries required for development and deployment


## Virtual Environment
Install the Conda
```sh
$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
$ chmod +x Miniconda-latest-Linux-x86_64.sh
$ ./Miniconda3-latest-Linux-x86_64.sh
    - Please input 'yes' to all
$ source .bashrc
    - If there is (base) in front of the command, it is a success.
$ sudo apt-get update
$ sudo apt-get upgrade
    - Please input 'y' to all
$ sudo apt-get install gcc
$ sudo apt-get install libmysqlclient-dev
    - Please input 'y' to all 
```
Create the virtual environment
```sh
$ conda create -n [project name] python==3.7
$ conda activate [project name]
```

## Installation from the git repo
```sh
$ git clone https://github.com/sayxyoung/eb-door-access-control-system.git
$ cd eb-door-access-control-system
$ pip install -r requirements.txt
```

## Setting the Django and RDS
Create a python file(my_settings.py)
```sh
$ cd ~/eb-door-access-control-system/
$ vim my_settings.py
```
Enter the code in my_settings.py
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'Project Database Name in RDS',
        'USER': 'RDS User Name',
        'PASSWORD': 'RDS User password',
        'HOST': 'RDS Endpoint',
        'PORT': '3306',
    }
}

SECRET_KEY = 'SECRET_KEY'
```

## Deployment using ElasticBeanstalk(EB CLI)
```sh
$ pip install awsebci
$ eb use [eb environment name]
$ eb status

$ git add .
$ git commit
$ git push

$ eb deploy
```

## API test results in Development Server
API test(integration test) used [POSTMAN](https://www.postman.com)<br>
The URL below is a document about integration test in develop server<br>
Please use chrome or safari<br><br>
[The Document about API TEST](https://documenter.getpostman.com/view/15151841/TzRX7jhm)

## How to use the api in Web Browser
Try using a deployed web api !<br>
Please check a document below for how to use the API<br><br>
[The Document about How to use the API and Credentials](https://www.notion.so/How-to-use-the-API-and-Credentials-abe527d55b844457950f1869905012b2) <br>
Below is the deployed web api address.<br>
[Web api address](http://ebdeploy.eba-mfzvps7e.us-east-2.elasticbeanstalk.com)

## ISSUE
I met and solved various issues during the project<br>
The URL below is a document about the issue in progress of the project<br><br>
[The Document about ISSUE](https://www.notion.so/Issue-c69283ce56f84063a62f34daef68ff1e)
 
