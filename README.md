# Application-Vprofile
This is a repository which has docker files to create a application which utilizes Web Server > App Server > Memcached > Database > Rabbit MQ

**You have to edit the application.properties file inside the tomcat application server** , 
1. Change the JDBC url - Update the Ip address of the database. Remember to use the Internal IP for communication,
2. Change the host of memcached server with the Internal IP
3. Change the host of rabbitmq server with the Internal IP

Below is the demo application properties file.

cat webapps/ROOT/WEB-INF/classes/application.properties
#JDBC Configutation for Database Connection
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://172.17.0.2:3306/accounts?useUnicode=true&characterEncoding=UTF-8&zeroDateTimeBehavior=convertToNull 
jdbc.username=root
jdbc.password=vprodbpass

#Memcached Configuration For Active and StandBy Host
#For Active Host
memcached.active.host=172.17.0.3
memcached.active.port=11211
#For StandBy Host
memcached.standBy.host=vprocache02
memcached.standBy.port=11211

#RabbitMq Configuration
rabbitmq.address=172.17.0.4
rabbitmq.port=15672
rabbitmq.username=guest
rabbitmq.password=guest

#Elasticesearch Configuration
elasticsearch.host =vprosearch01
elasticsearch.port =9300
elasticsearch.cluster=vprofile
elasticsearch.node=vprofilenode



**Update the nginx configuration with the correct Ip and url of the Tomcat server.**

root@vagrant:~/vprofile-project/Docker-files/web# cat nginvproapp.conf
upstream vproapp {
 server 172.17.0.5:8080;
}
server {
  listen 80;
location / {
  proxy_pass http://172.17.0.5:8080;
}
}
