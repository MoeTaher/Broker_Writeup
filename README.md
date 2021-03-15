# Broker_Writeup
![6bf0be37c0ab865c34fd3a3a547d0cb3](https://user-images.githubusercontent.com/58278761/111157858-092ae600-85a0-11eb-921e-cbbc339ad951.png)


Start with nmap ... 

![Screenshot from 2021-03-15 14-39-17](https://user-images.githubusercontent.com/58278761/111157962-2d86c280-85a0-11eb-8d92-9321d6d1ad5c.png)


we found that we have 2  Open ports , 1883 for the mqtt service and 8161 http for Activemq

Manually check the http, we got auth required for admin dir

![Screenshot from 2021-03-15 15-09-31](https://user-images.githubusercontent.com/58278761/111158482-bd2c7100-85a0-11eb-9598-03d03c148d5d.png)

Search for Default Creds for Activemq

![Screenshot from 2021-03-15 14-40-26](https://user-images.githubusercontent.com/58278761/111158542-cf0e1400-85a0-11eb-8e9c-0e4b3bea8d06.png)

you can find an interesting topic called "secret_chat"

![Screenshot from 2021-03-15 14-41-14](https://user-images.githubusercontent.com/58278761/111158805-23b18f00-85a1-11eb-8d83-aed79f07459e.png)

Use Mqtt client to Subscribe to the "secret_chat" and see the queued messages 

![Screenshot from 2021-03-15 14-44-03](https://user-images.githubusercontent.com/58278761/111159102-683d2a80-85a1-11eb-9c62-68da03ae5189.png)
# Foothold

Searching for Activemq CVE i found this github page for cve-2016-3088
https://github.com/coffeehb/Some-PoC-oR-ExP/tree/master/ActiveMQExP

![Screenshot from 2021-03-15 14-55-28](https://user-images.githubusercontent.com/58278761/111159682-09c47c00-85a2-11eb-9eeb-96eead312764.png)

![Screenshot from 2021-03-15 14-56-01](https://user-images.githubusercontent.com/58278761/111159718-147f1100-85a2-11eb-9de2-6ae945999430.png)

# Privilege Escalation 

checking the "sudo -l" first we Got this.. 

![Screenshot from 2021-03-15 14-58-31](https://user-images.githubusercontent.com/58278761/111159981-560fbc00-85a2-11eb-8db4-7bc1172470ad.png)

We can run subscribe.py as a root,
we check if we have a write permissions to the file.

![Screenshot from 2021-03-15 14-59-08](https://user-images.githubusercontent.com/58278761/111160168-848d9700-85a2-11eb-8b5e-8229d7db7cb7.png)

Yes we have!, now we can exploit it easly by adding shell in the file.

![Screenshot from 2021-03-15 15-00-44](https://user-images.githubusercontent.com/58278761/111160499-d20a0400-85a2-11eb-9766-c831ec735a32.png)

run the file. 

![Screenshot from 2021-03-15 15-01-17](https://user-images.githubusercontent.com/58278761/111160588-e948f180-85a2-11eb-9a3d-4f6aa92b09b7.png)

Have fun! :D



