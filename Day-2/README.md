KUBERNETES LABELS AND SELECTORS

LABELS:
•	 Labels  are used to organize K8S objects such as pods,nodes etc…
•	You can Add multiple lables over the Kubernetes objects
•	Labels are defined in key value pair
•	Labels are similar to tags in AWS, where you gave name to filter the resource quickly.
Suppose there are different pods.
I have created pods related to Swiggy app and Zomato app. If  I want to filter particular app pod. I create labels to that  pods while creating.

To create Label for Pod:
                   This is Pod related to Zomato
                   ![image](https://github.com/user-attachments/assets/a1f7cf47-2e49-4371-9b02-250032142cab)

              

Create a Pod related to Swiggy
             ![image](https://github.com/user-attachments/assets/f438268f-b53d-46a9-953b-f8eea103190a)

                    
To Create Pod 
            kubectl create -f  .  (By using This command created two pods at a time)
                 ![image](https://github.com/user-attachments/assets/3bb280ea-cd6b-429f-b58f-2d0663041022)

Two Pods Created
                         kubectl get pods
                         ![image](https://github.com/user-attachments/assets/021856b8-8cbf-4b97-9131-25418d852b5b)

 

To See labels of the pod
               kubectl get pods - -show- -labels
 
                 ![image](https://github.com/user-attachments/assets/6b35b533-f1cf-47ce-bcc7-8e96388c6f50)

To create a labels for exsiting pod
Suppose a create a pod without labels
   
  ![image](https://github.com/user-attachments/assets/ab793cb8-7616-468c-99dc-ce1a39e175ae)
  ![image](https://github.com/user-attachments/assets/ddf73814-3115-4043-816a-e94287cda73b)


          

Copy the ClusterIP of service and paste in any node in cluster.We access the app.
          




To Create a labels for existing pod
                  ![image](https://github.com/user-attachments/assets/73f68915-0316-4ba0-b870-345ece5c523a)
     

To filter a pods  
                    Suppose You want to  filter pods related to swiggy
                     kubectl  get pods -l project=swiggy
 
  ![image](https://github.com/user-attachments/assets/d5b23049-0c51-4def-9af1-f773564e5298)

If you want get pods except swiggy
                kubectl   get pods -l project!=swiggy
  ![image](https://github.com/user-attachments/assets/81610344-94a6-46ca-bdd0-0ca35dcc2b62)
        
           
SELECTORS:
•	 Selector helps us to filter the items/objects which have labels attached to them.
•	 Selectors are used to identify and select resources based on their labels.
•	They allow you to define a set of criteria that a resource must meet to be selected. Selectors are commonly used to define the desired state of a resource or to create relationships between different resources.
There are different types of selectors in Kubernetes:
Equality-based Selectors:
                       While Selecting a label if you are using equalsto(=)  or notequalsto(!=)  then it is eqaulity -based selector.
 
                   Here we can select only single label
 ![image](https://github.com/user-attachments/assets/09ea070d-bb00-450d-ade3-263ff35ee5c2)

 Set-based Selectors:
                                If you not used (=) and (!=) then it is Set-based selectors
                   Here we can select multiple labels
 

 ![image](https://github.com/user-attachments/assets/0a99dc9a-38f3-41db-89fc-616e93dc8f40)



                                                        SERVICES
•	Service is a method for exposing pods in your cluster
•	Each pod gets its own IP address but we need to access from IP of the Node.
•	If you want to access pod from inside (within the cluster)  we use ClusterIP
•	If you want to expose application to external we use NodePort and Load Balancer

Types
•	CLUSTER-IP
           ClusterIP is an internal IP type, accessible only within the cluster. This type is assigned to a service when you don’t explicitly specify the type in the YAML file. It’s suitable when your application should only be accessed within the cluster, ensuring internal communication. It’s like an internal phone line for services to communicate with each other.
 
                 By using this we can access app within the cluster

•	NODEPORT
                   By using NodePort, you can access a service with the NodePort type from outside the cluster. This is achieved by sending a request to any of the nodes in the cluster using the specified node port. The node will then forward the request to the appropriate service, which in turn directs the request to the pods associated with that service. Consequently, the service becomes accessible from outside the cluster.
          To access the app on internet we use NodePort and LoadBalancer

•	LOAD BALANCER
                                         It is an extension type of the nodeport service. When using a LoadBalancer service type, incoming traffic from the external world is directed to the load balancer's external IP. The load balancer then routes the traffic to the appropriate nodes and their respective ports based on the defined rules, typically using the NodePort allocated for the service on each node. This abstraction adds an extra layer and ensures that traffic is managed and distributed efficiently across the nodes in the cluster. Direct access to a node from the external world is not typical or intended with a LoadBalancer service type.
              By using  LoadBalancer we can expose app to external,using cloud providers load balancer.This type of service is used when app typically handle high traffic loads



EXAMPLES:
ClusterIP
Create two yml files
a)	Pod yml file named as firstapp.yml
 ![image](https://github.com/user-attachments/assets/4cc22ff4-b895-48cf-831e-73e531c66158)

b)	Service Yaml file named as serviceapp.yml
 ![image](https://github.com/user-attachments/assets/77e2dd72-6ce1-4374-9637-e3c9497cc61c)
 ![image](https://github.com/user-attachments/assets/4f40e3c0-62a6-467e-8970-f0320ac9958d)

 

In service yml file I mentioned type as ClusterIP.
  
By using ClusterIP we can acces app within the cluster.We can’t acces from it outside.
               curl cluster_ip
![image](https://github.com/user-attachments/assets/b31e29a9-0c7a-4918-80e9-a205a721990b)

curl 100.70.227.103  

Node 1:
![image](https://github.com/user-attachments/assets/d4ebd901-6fea-4e13-9426-181cad3af564)

 


Node 2 : 

![image](https://github.com/user-attachments/assets/375c60f5-6f8d-4898-9a7a-01982ae13a6b)
 

NODE PORT:
           To expose app to external we use NodePort

![image](https://github.com/user-attachments/assets/be10dacc-1bc3-4ce0-aebe-fe67ce24b021)
          
Service is created with NodePort
![image](https://github.com/user-attachments/assets/be9b7dad-f71d-4cfc-b33d-5c6fa0e81b2b)
   
                  
Copy the Port of Nodeport and Paste in Browser with with public_ip of server
![image](https://github.com/user-attachments/assets/65574143-f418-427c-9dcf-5cb8547cfe80)
           

         I Successfully accessed from external (internet) by using NodePort 🥳


LOAD BALANCER:
     By using  LoadBalancer we can expose app to external,using cloud providers load balancer.This type of service is used when app typically handle high traffic loads
          
![image](https://github.com/user-attachments/assets/b2ce7e96-fa70-4527-a198-e71c03e67b3d)
![image](https://github.com/user-attachments/assets/b7b82691-9be3-48a7-b238-45ece15ddc04)
                

Copy the External IP of Load Balancer access application

        
![image](https://github.com/user-attachments/assets/df7b428c-ef3f-425e-97ea-e84681571c88)
