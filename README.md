# Apache ACE Target Template for OpenMUC

This project provides a target template for using OpenMUC with the software distribution framework [Apache ACE](https://ace.apache.org/).
Putting together the power of OpenMUC for monitoring and control systems with the possibility to distribute software (updates) to a 
large number of on-premise clients allows scenarios like:

* Individual test setups for both, developers and software testers
* Initial provisioning of new OpenMUC installations, even directly on customer premises
* Centralized deployment of software updates without restart of the client systems (hot deployment)
* Centralized management of deployed features individually for each customer

The template currently uses Apache ACE 2.1.0. General information about ACE can be found in the [ACE user guide](https://ace.apache.org/docs/user-guide.html). 

## Licenses
The files of this project have different sources and are protected by different licenses:
* The `run-openmuc.sh` file as well as all files in the `/conf` directory come from the [OpenMUC project](https://www.openmuc.org/) and are licensed under GNU GENERAL PUBLIC LICENSE Version 3.0
* The ACE agent library `com.apache.ace.agent.jar` comes from the [Apache ACE project](https://ace.apache.org/) and is licensed under Apache License, Version 2.0
* The Apache Felix OSGi framework comes from the [Apache Felix project](http://felix.apache.org/) and is licensed under Apache License, Version 2.0

All other work of this project including the documentation is licensed under Apache License, Version 2.0.

## Configuration
The configuration of the ACE agent bundle can be set inside the [config.properties](conf/config.properties) file. This template includes the most common parameters preconfigured in the file. If any value is set, it's the default value. For a more detailed description of the parameters see the [ACE user guide](https://ace.apache.org/docs/user-guide.html#target-configuration). To start, at least the following both parameters must be set:

```
agent.identification.agentid=openmuc-1
agent.discovery.serverurls=http://localhost:8080
```
The`agentid` parameter sets the identification of the target. It must be unique for each ACE server instance. The `serverurls` parameter defines one or more urls of the central ACE servers.

## Deployment
Bundles deployed to the target will be stored in the cache directory of the OSGi framework (`felix-cache` by default). The default setting of Felix in OpenMUC clears the cache on startup of the framework and installs and starts all bundles from the `/bundles` folder afterwards. This behavior deletes all centrally deployed bundles. To prevent the cache from being flushed, the following setting in the `config.properties` file must be set:

```
org.osgi.framework.storage.clean=none
```

## Known limitations
Out of the box, ACE can only handle OSGi bundles and .cfg configuration files. It's not possible to distribute other artifacts like the `channels.xml` file. Adding support for new types of artifacts is possible, more details can be found in the [documentation](https://ace.apache.org/docs/adding-custom-artifact-types.html). Because of this, an empty `channels.xml` file is part of this template. If not provided to the OpenMUC framework, an error occurs.
