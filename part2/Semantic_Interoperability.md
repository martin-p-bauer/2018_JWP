# Semantic Interoperability Across Systems [Antonio Jara]
How to achieve semantic interoperability across systems.

# Semantic interoperability by ontological models [Jaeho Lee]

**1. Request to report**
![Request to report](./../img/JHL-Request2Report.png)


**Service Executor (Apache Jena code)**

```java

handleRequest(Request r){	
	OntClass requestService = currentServiceModel.getServiceByName(r.name());
	Individual[] homeControlSystems = currentUserModel.getUserHomeService(requestService);
	for(OntIndiv system : homeConstrolSystem){
		String service = system.getServiceName();
		String arg = system.getServiceArgument(r.getArgument);
		systemConnector.set(service,arg);
	}
}

```

**Semantic Mapping (Apache Jena code)**

```java
handleRequest(Request r){	//Semantic Mapping
	OntClass requestService = currentServiceModel.getServiceByName(r.name());
	Individual deviceSystems = currentDeviceModel.getDeviceService(requestService);

	String service = deviceSystem.getServiceName();
	String arg = deviceSystem.getServiceArgument(r.getArgument());

	device.execute(service, arg);
}
```

**Information Mapping (Apache Jena code)**

```java
handleCommand(Command c){ //Information Mapping
	OntClass serviceCommand = currentDeviceModel.getCommandByName(c.name());
	Individual[] deviceCommands = currentDeviceModel.getDeviceCommand(serviceCommand);]
	for(Individual command : deviceCommands){
		String command = command.getCommandName();
		String argumentAspect = command.getCommandAspectFromName(command);
		
		String argumentValue = command.convertArgumentByAspect( getCommandArgument(c.getArgument()) , argumentAspect);
		String deviceURI = command.getDeviceURI();

		DeviceManager.sendRequest(deviceURI, command, argumentValue);
	}
}
```


**2. Status Report**
![Status report](./../img/JHL-StatusReport.png)



**3. Request to control**
![Request to control](./../img/JHL-Request2Control.png)

