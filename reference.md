Here are a few of my commonly used things:

## MySQL
* Enable account for remote connection:
 ```
    GRANT ALL PRIVILEGES ON *.* TO 'user'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
    FLUSH PRIVILEGES;
 ```
* Remote dump:
 ```
    mysqldump -u 'user' -h 'host' -P 'port' -p 'target DB' > 'target file'
 ```
* Remote dump (docker):
 ```
    docker exec CONTAINER /usr/bin/mysqldump -u root --password=pw DATABASE > db.sql
 ```
* Remote connect:
```
    mysql -u 'user' -h 'host' -P 'port' -p  
```

* Show all unique Triage dates from trip
```
select DISTINCT DATE(date_of_triage_visit) as dotv from patient_encounters ORDER BY dotv DESC;
```
* Show all unique Triage dates from trip with a sum for how many encounters were on each date
```
select DISTINCT DATE(date_of_triage_visit) as dotv, COUNT(*) from patient_encounters GROUP BY dotv DESC;
```
* Get patient encounter count between dates
```
select count(*) from patient_encounters WHERE date_of_triage_visit > '2017-06-13';
```
* Retrieve unique patient count prior to a particular encounter (isolating trips)
```
select DISTINCT(patient_id) from patient_encounters where id < 100443;
```


## Linux
* Remote scp files:
```
    scp -r 'user'@'host':/opt/femr/..../Upload .
```  
* Recursive find & replace
```
    find ./ -type f -exec sed -i -e '/s/replace/me/g' {} \;
``` 

## Docker
* Start up container:
```
     docker run -p 3306:3306 --name femr -e MYSQL_ROOT_PASSWORD=password -d mysql:5.6.35
```     
* OpenSSL encrypt/decrypt with password (use key for real security)
   Encrypt:
```
     openssl aes-256-cbc -a -salt -in secrets.txt -out secrets.txt.enc
```   
   Decrypt:
```   
     openssl aes-256-cbc -d -a -in secrets.txt.enc -out secrets.txt.new
```  

