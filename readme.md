
#Service Registry and Discovery Using HashiCorp Consul

##setting up the consul server
 -[consul Download](https://developer.hashicorp.com/consul/downloads?host=www.consul.io)
 -Download the file based on required os.Extract the file consul.exe and set the path so that it can be acessed with command prompt.
 -The server can be started in two ways
 +First in debug mode using command "consul.exe agent -dev".
 +Second in Release mode "consul.exe agent -server -bootstrap -config-file="config.json".
 +config-file
  {
  "datacenter": "name",
  "data_dir": "Directory of the consul", 
  "log_level": "INFO", 
  "node_name": "node1",  
  "server": true,
  "bind_addr":"Ip_Address",
  "ui":true,
  "log_file":"Directory or path of the log file"
}
-server starts at localhost:8500

##Golang

-Import the library "github.com/hashicorp/consul/api".
cmd:go get "github.com/hashicorp/consul/api"
###Service Registry
-Default config file can be made using Defaultconfig()
-Create a New Client using the Default config as parameter.
-Next specify the details as service Id,Port No,Host Name which are required for the service registration.Recomended to Include check.
-Using the consul.Agent().ServiceRegister(registration) the registration can be registered.
-Check function can be implemented to get responses.
###Client Discovery
-Default config file can be made using Defaultconfig()
-Using consul.Agent().Services() we get the list of services that are connected to server as a map.
-we can the take a particular instance using the instance id 
ex:services["instance-id"]
-we can get the adress and port from the service which can be used to redirect to that instance.

##Java

###Service Registry
-Create a Spring Starter Project With the dependencies spring web and consul discovery for Service Registry.
-In application.properties set the following variables:
+spring.application.name //The name of the application 
+server.port //The Port on which the server is running
+spring.cloud.consul.discovery.hostname //The Host Name 
Application can be started as a java application with the restController implementations.

###Client Discovery
-Annotation used:@EnableDiscoveryClient
-For fetching URI:URI uri=client.getInstances("Instance ID").stream().map(si->si.getUri()).findFirst().map(s->s.resolve("/Path to be appended after the url of the instance fetched")).get();


