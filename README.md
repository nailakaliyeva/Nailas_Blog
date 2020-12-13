This project has already been deployed and is running live on [www.nailasblog.com](www.nailasblog.com)
The blog is user friendly and pretty intuitive. I'm using a free Mailgun API to send recovery emails to users 
who have forgotten their passwords. 

⚠️ When it comes to resetting passwords, there are a couple of things both 
***users*** and ***devs*** should know if they run into an error after clicking 'Request Password Reset' button 
(⚠️ only for Gmail users):
1. You need to allow access to less secure apps to be able to receive a password recovery email from the website
![Screenshot (1529)](https://user-images.githubusercontent.com/42359973/102000584-e47c5500-3cb6-11eb-811f-ed5b21e9f404.png)
2. Try unblocking your IP (sometimes it gets blocked by Google) by visiting [https://accounts.google.com/DisplayUnlockCaptcha](https://accounts.google.com/DisplayUnlockCaptcha)

For ***devs***

If you want to **copy the project from GitHub** simply run:
```
$ git clone /path/to/repository
```

However, if you want to **copy the project from your local machine**, use the secure copy command:
```
$ scp -r Desktop/or/wherever/your/project/located/on/your/comp root@11.11.111.11(your remote IP): ~/Project/folder
```
To **create a virtual environment** to run the application run:
```
$ sudo apt install python3-pip
```
*then*
```
$ sudo apt install python3-venv
```
*then*
```
$ python3 -m venv Project_folder/venv
```
*then*
```
$ source /venv/bin/activate
```
from within your project folder to **activate your virtual environment**

Run:
```
$ pip install -r requirements.txt
```
**to install all the packages needed to run the application**

**To install nginx** to handle the front end run: (make sure you're also doing this within your venv)
```
$ sudo apt install nginx
```
**To restart nginx** run:
```
$ systemctl stop nginx
```
```
$ systemctl restart nginx
```
**To install gunicorn** to handle the python files run: (make sure you're also doing this within your venv)
```
$ pip install gunicorn
```

**To restart gunicorn** run:
```
$ pkill gunicorn (**to first kill gunicorn**)
```
Make sure you activate your virtual environment when inside the project folder by running
```
$ source /venv/bin/activate
```
*then* run the actual command **to start gunicorn**
```
$ gunicorn -w 3 run:app 
```
(where 3 is number of cores on your remote machine times 2 plus 1. 
**To find out the num of cores on your remote machine** run 
```
$ nproc --all)
```
**To install supervisor** to monitor our gunicorn run: (make sure you're also doing this within your venv)
```
$ sudo apt install supervisor
```
**To reload supervisor** run:
```
$ sudo supervisorctl reload
```
If you have any requests errors associated with /users/routes.py, (which also takes care of your reset password function)
then you would find them in the requests.log file within the project folder
If you have any application errors, you will find them within ~/var/log/flaskblog/flaskblog.err.log file

Remember that if you want to run this project from GitHub you would need to transfer all your environment variables
to .env file from the config.json file they are currently in on the remote computer AND 
replace 'current_app.config['API_KEY']' on line 29 in users/utils.py with os.getenv('API_KEY')

**To check uncomplicated firewall status** and to SEE allowed ports run:
```
$ sudo ufw status
```
**To change some default traffic settings** run:
```
$ sudo ufw default allow outgoing 
```
*OR/AND*
```
$ sudo ufw default deny incoming 
```
**to allow outgoing or deny incoming traffics** respectively

**To allow certain ports** run:
```
$ sudo ufw allow #### (where #### is the port number)
```
**To disallow certain ports** run:
```
$ sudo ufw delete allow #### (where #### is the port number)
```
**To enable all the ufw rules** run:
```
$ sudo ufw enable
```
You have to be added as the user of sudo group by the root or be the root yourself to add or delete ufw rules

If you want **to kill certain ports** run:
```
$ fuser -k #### (where #### is the port number)
```
Other than that, I used Jinja2 just to practice, however, I strongly support front end done with React components rather 
than  barebone HTML/CSS/Bootstrap because I find React more efficient and sophisticated. 
