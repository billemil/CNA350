# CNA350
##Necessary Components:
###VM with the following installed:
	docker
	docker-compose
###Images:
	phpmyadmin
	mariadb

##Prepare VM to run code:
	
Clear existing images/containers
'''
>docker system prune -a
'''

Clone repository:
>git clone https://github.com/billemil/CNA350

Navigate to maxscale directory:
>cd CNA350/maxscale

Edit images within docker-compose.yml to use latest versions:
>sudo nano docker-compose.yml
	ie. mariadb:10.3 --set to--> mariadb:latest 

Run the docker-compose.yml :
>sudo docker-compose -f "docker-compose.yml" up -d --build

Confirm Shard-A and Shard-B are Running:
>docker-compose exec maxscale maxctrl list servers 
#Will print a visual table

Install requirements to use mysql commands:
>sudo apt install mariadb-client-core-10.1

Confirm databases:
>mysql -u maxuser -pmaxpwd -h 127.0.0.1 -P 3306 -e "show databases"

Query Shards/Zipcodes:

TEST Zipcode1:
>mysql -u maxuser -pmaxpwd -h 127.0.0.1 -P 3306 -e "SELECT *  FROM zipcodes_one.zipcodes_one LIMIT 50;"

TEST Zipcode2:
>mysql -u maxuser -pmaxpwd -h 127.0.0.1 -P 3306 -e "SELECT *  FROM zipcodes_two.zipcodes_two LIMIT 50;"

#help received from sam and brandon during this project
