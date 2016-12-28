# Apache ACE Target Template for OpenMUC

This project provides a target template for using OpenMUC with the software distribution framework [Apache ACE](https://ace.apache.org/).
Putting together the power of OpenMUC for monitoring and control systems with the possibility to distribute software (updates) to a 
large number of on-premise clients allows scenarios like:

* Individual test setups for both, developers and software testers
* Initial provisioning of new OpenMUC installations, even directly on customer premises
* Centralized deployment of software updates without restart of the client systems (hot deployment)
* Centralized management of deployed features individually for each customer

The template currently uses Apache ACE 2.1.0. General information about ACE can be found in the [ACE user guide](https://ace.apache.org/docs/user-guide.html). 

## Configuration
The configuration of the ACE agent bundle can be set inside the [config.properties](conf/config.properties) file. This template includes the most common parameters preconfigured in the file. If any value is set, it's the default value. For a more detailed description of the parameters see the [ACE user guide](https://ace.apache.org/docs/user-guide.html#target-configuration). To start, at least the following both parameters must be set:

```
agent.identification.agentid=openmuc-1
agent.discovery.serverurls=http://localhost:8080
```
The`agentid` parameter sets the identification of the target. It must be unique for each ACE server instance. The `serverurls` parameter defines one or more urls of the central ACE servers.
