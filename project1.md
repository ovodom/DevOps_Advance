# PROJECT 1: ANSIBLE CONFIGURATION TASKS.
## To execute this project:
1.	Five instances opened.



![img](img/img1.png)



2.	Ssh to the ansible instance terminal and generate key pair using the command ```ssh-keygen``` to get the key pair and press on enter key till it gets off from the key enviroment .



![img](img/img1a.png)


![img](img/img2.png)


![img](img/img3.png)



3.	Enter the command ```ls ~/.ssh``` to show keys that are within the terminal- authorized_keys, private and public key. 



![img](img/img4.png)




![img](img/img5.png)



4.	Use ```cat /home/Ubuntu/.ssh/pub key``` to highlight the public key. Copy and save it. 




![img](img/img6.png)




5.	Ssh to the webserver1 terminal, generate ssh key pair with ```ssh-keygen``` command, and list keys located in the terminal.



![img](img/img7.png)



![img](img/img8.png)




6.	Link webserver1 with Ansible instance by configuring webserver1 with the command ```vi ~/.ssh/authorized_keys```.


![img](img/img9.png)




7.	Delete the default key there and paste the ansible public key (initial key copied) and save it. Do the same for the other servers (webserver2, database1, and database2).



![img](img/img10.png)



![img](img/img11.png)




8.	Try the connection with ssh ip address of any of the servers. e.g ssh 172.32.25.190



![img](img/img12.png)




9.	Use the mkdir ansible to create the directory ansible on the ansible terminal.



![img](img/img13.png)




10.	cd ansible to access the directory ansible.
a.	Apply ```vi inventory``` commanad to create inventory file in ansible directory
b.	Paste ip address of the various servers here, grouping them into webservers and database servers.
c.	```cat inventory``` to read the inventory file.



![img](img/img14.png)




11.	Run an ansible adhoc command, ansible –i inventory all “shell” –a “touch ansibletest.txt”



![img](img/img14.png)



![img](img/img16.png)




12.	Two ansible playbooks created. Enter command to create playbook ```vi myplaybook1.yml```, ```vi myplaybook2.yml```. Playbook here named myplaybook1 and myplaybook2



![img](img/img17.png)




13.	 On the playbook configuration page place YAML language instructions to carryout tasks on the webservers and database servers and save the scripts.



![img](img/img18.png)



![img](img/img19.png)



![img](img/img20.png)




14.	    To run the ansible playbooks created (myplaybook1 and myplaybook2) use the following command, 
```ansible-playbook -i inventory myplaybook1.yml``` and ```ansible-playbook -i inventory myplaybook2.yml```.



![img](img/img23.png)




15.	Successful run. Outcome shows successful creation of apache and nginx on the webservers and database servers, disk space and available memory seen on the terminal.



![img](img/img24.png)



![img](img/img25.png)



![img](img/img26.png)



![img](img/img27.png)



![img](img/img28.png)



A close look at the commands entered on numbers 11 & 13, you discover that 11 has one command and it was on the terminal, which is a one of. As for 13 you find out it is a series of command in YAML language which are linked to form a task or various task. Note: it is reusable. In conclusion 11 is ansible an adhoc command while 13 are contained ansible playbooks.
