# Network Security using ACL


## Description

In our Network we will work with 3 Pt-routers, 4 switches  and some devices. 

![image](https://user-images.githubusercontent.com/73224547/224576570-89f33ac1-79cb-45f7-ba77-ed58eff7a2de.png)

## Router,Switch configuration

This configuration sets up three interfaces on the router, two FastEthernet interface with an IP address of 200.4.1.1/24 and 200.4.2.1,  one Serial interface with an IP address of 200.4.5.1/24. Both interfaces are enabled with the no shutdown command. Finally, we can add  the copy running-config startup-config command saves the configuration to non-volatile memory so that it will persist across reboots or The description command is used to add a description to an interface in a router configuration..

![image](https://user-images.githubusercontent.com/73224547/224576772-0b4fc1cc-805c-44bb-a223-7beefac37322.png)
![image](https://user-images.githubusercontent.com/73224547/224576867-a38f8352-a6fe-4c1a-a1a1-04c10958001b.png)
![image](https://user-images.githubusercontent.com/73224547/224576878-39a43e3c-e07e-45b7-9fd6-88e5412498ef.png)


For the others routers I used the gui config, it's usefull and fast.

for the second router R2 , two   Serial interface interface with an IP address of 200.4.5.2/24 and 200.4.6.1,  one FastEthernet with an IP address of 200.4.3.1/24.


![image](https://user-images.githubusercontent.com/73224547/224577198-f2b916b8-d298-4ca2-8fd7-2d051b816055.png)
![image](https://user-images.githubusercontent.com/73224547/224577207-d35b0bc0-0a85-4001-8acf-e9ec3fec29c0.png)
![image](https://user-images.githubusercontent.com/73224547/224577214-2b6223be-7eb7-4e19-acfe-b43b0ef0febd.png)

for the third router R3 , one Serial interface interface with an IP address of 200.4.6.2/24 and  one FastEthernet with an IP address of 200.4.4.1/24.

![image](https://user-images.githubusercontent.com/73224547/224577359-97135cdb-9bfa-4f83-8d83-e9dded9f8058.png)
![image](https://user-images.githubusercontent.com/73224547/224577370-049a55bc-9223-47b6-95df-f5761a7b06b1.png)

after we gave every Device his ip address, either using the switch or using config.
- example

![image](https://user-images.githubusercontent.com/73224547/224577505-0c804044-8120-44fb-ad1b-1a03be9073db.png)

## Routing

Routing is the process of forwarding data packets between different networks in order to deliver them to their intended destinations. In order to use routing in a network, you need to configure the routers that connect the different networks.

Enable routing on each router using the ip routing command. This tells the router to forward packets between networks

For the first Router R1

![image](https://user-images.githubusercontent.com/73224547/224577781-91e8a5ce-d5fe-4424-a68a-71d06f4b9419.png)


For the second one R2

![image](https://user-images.githubusercontent.com/73224547/224577797-a172d0f4-78f4-4786-b6e1-1a8a06f973d2.png)

For the second one R3

![image](https://user-images.githubusercontent.com/73224547/224577812-593945a1-3b32-4198-aba3-6246b3614a4f.png)


- A simple test using ping.

![image](https://user-images.githubusercontent.com/73224547/224578336-fb0943c0-eb8a-4b6d-a539-3ee351657828.png)

## ACL
- 1 
To allow packets to be sent from the machine with IP address 200.4.1.2 and deny packets from the machine with IP address 200.4.1.3 going to the network 200.4.3.0, you can use Access Control Lists (ACLs) in the router configuration.

![image](https://user-images.githubusercontent.com/73224547/224578716-614ec899-89d0-4453-85d8-867cd5ee972e.png)


In this example, ACL 1 is created with two rules. The first rule allows packets from the machine with IP address 200.4.1.2. The second rule denies packets from the machine with IP address 200.4.1.3 going to the network 200.4.3.0.

Next, you can apply this ACL to an interface on the router to control traffic passing through it. For example, to apply ACL 1 to the interface connected to the network 200.4.3.0

- Test
Allowed

![image](https://user-images.githubusercontent.com/73224547/224578990-9adcecea-4e1c-42ff-8eae-f9938e29de45.png)

![image](https://user-images.githubusercontent.com/73224547/224578993-c29ed3cd-675f-4b6e-a6ef-a8178413a0c7.png)

Denied

![image](https://user-images.githubusercontent.com/73224547/224579032-830477f7-98ee-41cf-95df-f6ba8fbb4bf5.png)

![image](https://user-images.githubusercontent.com/73224547/224579045-235c22f0-8e54-4b71-abd7-3591410b2774.png)


 the ACL is applied to the outbound traffic on FastEthernet0/0 interface. This means that the ACL is applied to the traffic leaving the router and going towards the network 200.4.3.0. The ACL will allow packets from 200.4.1.2 and deny packets from 200.4.1.3 going to 200.4.3.0.


- 2 To deny packets from the machine with IP address 200.4.3.3 going to the networks 200.4.2.0 and 200.4.1.0, you can use an Extended Access Control List (ACL) in the router configuration.


![image](https://user-images.githubusercontent.com/73224547/224579268-d204adf7-2c8a-4650-a4b0-1d188e096c92.png)

In this example, ACL 100 is created with two deny rules and a permit any rule at the end. The first two rules deny packets from the machine with IP address 200.4.3.3 going to the networks 200.4.2.0 and 200.4.1.0. The third rule permits all other traffic.

Next, you can apply this ACL to an interface on the router to control traffic passing through it. For example, to apply ACL 100 to the inbound traffic on Se2/0 interface.

- Test Denied

![image](https://user-images.githubusercontent.com/73224547/224579366-a4176db6-c7b5-4e02-a6f3-49501250c1f6.png)

![image](https://user-images.githubusercontent.com/73224547/224579372-c06f0ae2-b3fb-4d50-9b84-9713a4f41e73.png)

- 3 To deny packets originating from the network 200.4.4.0 and going to the network 200.4.3.0, you can use an Extended Access Control List (ACL) in the router configuration.

![image](https://user-images.githubusercontent.com/73224547/224579689-59b80edb-616a-4efe-add4-43bb15681eca.png)

In this example, ACL 103 is created with a deny rule and a permit any rule at the end. The first rule denies packets originating from the network 200.4.4.0 and going to the network 200.4.3.0. The second rule permits all other traffic.

Next, you can apply this ACL to an interface on the router to control traffic passing through it. For example, to apply ACL 103 to the outbound traffic on Fa0/0 interface.



- Test

In this example, the ACL is applied to the outbound traffic on Fa0/0 interface. This means that the ACL is applied to the traffic leaving the router towards the network 200.4.3.0. The ACL will deny packets originating from the network 200.4.4.0 and going to the network 200.4.3.0.

![image](https://user-images.githubusercontent.com/73224547/224579874-985e1cd2-0b58-4ec8-aea0-b70892884697.png)

![image](https://user-images.githubusercontent.com/73224547/224579878-c800138f-72b9-4ab1-9024-acc733d34a4d.png)


- 4 To deny pings originating from the network 200.4.2.0 and going to the network 200.4.1.0, and only allow pings from the machine with IP address 200.4.2.3, you can use an Extended Access Control List (ACL) in the router configuration.

![image](https://user-images.githubusercontent.com/73224547/224580265-840e26b9-5f98-40da-9d99-cb42137e7764.png)


In this example, ACL 104 is created with two deny rules and a permit any rule at the end. The first rule denies ICMP packets (pings) originating from the network 200.4.2.0 and going to the network 200.4.1.0. The second rule permits ICMP packets (pings) from the machine with IP address 200.4.2.3 going to the network 200.4.1.0 with the "echo-reply" message type. The third rule permits all other traffic.

Next, you can apply this ACL to an interface on the router to control traffic passing through it. For example, to apply ACL 104 to the inbound traffic on Se2/0 interface.

- Test


In this example, the ACL is applied to the inbound traffic on Se2/0 interface. This means that the ACL is applied to the traffic entering the router from the network 200.4.2.0. The ACL will deny pings originating from the network 200.4.2.0 and going to the network 200.4.1.0, and only allow pings from the machine with IP address 200.4.2.3.

![image](https://user-images.githubusercontent.com/73224547/224580038-60ecba0a-add9-4c24-a59f-2a13a794b91a.png)



