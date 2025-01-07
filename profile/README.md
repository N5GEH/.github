![ERC](https://raw.githubusercontent.com/RWTH-EBC/FiLiP/master/docs/logos/EBC_Logo.png) ![TUD](/logos/Logo-Banner-TUD-IET-GEWV.jpg?raw=true)

# Welcome to the N5GEH GitHub Presence
In the following, we briefly describe our provided repositories containing tutorials, tools, services and device software. The repositories have been created in the course of the [N5GEH-Serv](https://n5geh.com/) project and its predecessor N5GEH. In the [N5GEH project network](https://n5geh.com/project-network/), projects from different areas in the energy sector committed themselves to base their applications on the [FIWARE open source platform framework](https://github.com/FIWARE/catalogue). 
In our repositories, we provide generalized solutions for the N5GEH project network.

If there are any questions or remarks, feel free to leave an issue or contact us directly. 

## N5GEH platform 
The [n5geh.platform](https://github.com/N5GEH/n5geh.platform/tree/master) repository walks you through the setup of a possible FIWARE-based platform, both in single node and multi node setup. We applied additional tools and platform settings recommended by us. We simply refer to the used setup as platform.
Of course, this is just one possible solution. FIWARE follows the approach of a modular framework so you can build your plattform according to your needs. So you can exchange components, simply add new ones or delete obsoletes ones in order to build the platform customized for your use case.
Our basic platform setup includes the commonly used orion context broker as central component for context management. Orion is stateless and saves its data in MongoDB. We apply IoT agents in order to provide MQTT, AMQP and HTTP bindings towards the field layer. For the commonly used MQTT protocol, we set up the MQTT broker called mosquitto. In order to save timeseries data, we use Quantumleap that functions as an NGSI interface to timeseries databases like CrateDB or TimescaleDB. In our example, we use CrateDB. To visualize data saved in CrateDB, we use grafana.
![picture](/logos/platform_overview_simple_600dpi.png?raw=true)

NGSI comes in two different versions: Version 2 (NGSIv2) and Linked Data (NGSI-LD). NGSI v2 is the legacy version but still offers some functionalities NGSI-LD has not implemented yet. Nevertheless, NGSI-LD is the standardized format by the European Telecommunications Standards Institute (ETSI) that is under constant development. 

We encourage users interested in using NGSI-LD but are not familiar with platforms, REST APIs, JSON or the concept of linked data to start with the NGSIv2 setup and learn about NGSI and the platform's capabilities.

## Tutorials 
In the [n5geh.tutorials.from_sensor_to_application](https://github.com/N5GEH/n5geh.tutorials.from_sensor_to_application), we give an overview on how devices and simulations can be connected to the platform. We also show how to create a PID controller based on one of our frameworks, a control framework. With this controller, we control a building's zone temperature data within a simulation. Last, we visualize the data in grafana.

In the [n5geh.tutorials.data_model](https://github.com/N5GEH/n5geh.tutorials.data_model) tutorial, we showcase how to create data models for specific use cases and integrate these models with FIWARE-based platforms.
Examples in various domains are provided, including **Buildings automation**, **Electrical grid operation and monitoring**, and **District heating**.
These examples are given in form of Jupyter Notebook.

The [n5geh.tutorials.mosquitto_with_oauth2](https://github.com/N5GEH/n5geh.tutorials.mosquitto_with_oauth2-) tutorial explains the configuration for a mosquitto MQTT broker in order to let a keycloak server handle the authentication and authorization for MQTT clients based on the openID connect protocoll. You need to implement authentication and authorization for your devices to protect your platform. Otherwise, unauthorized devices can feed your platform with false data or even worse flood the databases in a denial of service attack. Mosquitto itself comes with internal ways to handle authentication and authorization. Yet, we provide an additional way in using keycloak as external identity and access management. This comes in handy when you want to adapt device information on the fly.

In the [n5geh.tutorials.route_and_secure_applications](https://github.com/N5GEH/n5geh.tutorials.route_and_secure_applications) tutorial, keycloak gatekeeper is used as Policy Enforcement Point (PEP) Proxy to secure certain services, APIs, and ports. Furthermore, we use the reverse proxy Traefik to route incoming requests based on DNS to the corresponding docker service. Traefik allows easy integration and discovery with docker. 

**Note:** Gatekeeper is not longer maintained by keycloak. We shifted to another very popular open source proxy that is also recently used by FIWARE Technical Experts: Kong. We show how to use it in the following tutorial.

The next repo shows how to protect your services, APIs, and ports using the Kong API Gateway working as PEP proxy. It communicates with a keycloak server for authentication and authorization of incoming requests [n5geh.tutorials.api-protection](https://github.com/N5GEH/n5geh.tutorials.api-protection). We provide several plugins in order to cover basic authentication and authorization use cases. Have a look at the repository for further information.

## Tools
### Entirety
Entirety is a web service written in Django that provides a graphical user interface to provide FIWARE users an easy access to the FIWARE core components without being familiar with REST requests and the FIWARE internal data handling. Entirety offers modules to create, read, update and delete devices, entities and notifications. Furthermore, Entirety comes with a module to visualize the relationships between your entity data. Currently, Entirety supports the FIWARE internal format NGSIv2 but we are already working on a NGSI Linked Data support.
Entirety can be found in [n5geh.tools.entirety](https://github.com/N5GEH/n5geh.tools.entirety). 

We provide a quick step-by-step tutorial to set up Entirety in [tutorials.entirety_step_by_step](https://github.com/N5GEH/n5geh.tutorials.entirety_step_by_step) tutorial can be used. 

### FiLiP

[FiLiP](https://github.com/RWTH-EBC/FiLiP) is a python software development kit for accelerating the development of web services that use certain Fiware's Generic Enablers (GEs) as backend. FiLiP allows you to interact with the GEs without deeper knowledge how to communicate with their APIs.

### MQTT Gateway 
[n5geh.tools.mqtt-gateway](https://github.com/N5GEH/n5geh.tools.mqtt-gateway) provides a universal interface that can integrate any MQTT-based JSON data into NGSI-V2 context broker.

### Cratesweep 
[n5geh.tools.cratesweep](https://github.com/N5GEH/n5geh.tools.cratesweep) is designed to regularly clean up CrateDB tables based on configured intervals. This might be useful if you have limited storage or need to clearn certain dummy data regularly.

## Services
### Controller 
[n5geh.services.controller](https://github.com/N5GEH/n5geh.services.controller) contains a generic PID controller framework to control IoT devices that are connected to a FIWARE platform via Orion context broker.

### Grid Protection 
The [n5geh.services.grid_protection](https://github.com/N5GEH/n5geh.services.grid_protection) repository serves as an exemplary implementation of cloud-based grid protection. 
This use case represents a supplementary protection scheme in the low and medium voltage electrical grid. The use case grid protection aims on mobile network communicaton based on very low end-to-end latency (1 – 10 ms) as well as easy-to-integrate back-up protection and can be seen as feasibility evaluation of the 5G standard. 
Nowadays in low voltage (LV) grids, the number of connected decentralized generators (DGs) and battery storages, respectively, is still rising. Thus, a decrease of the gap between maximum operating current and minimum short circuit current occurs. In addition to this, the short circuit current (SCC) contribution from DGs in inverter dominated grids can lead to so-called "Blinding" or “Sympathetic Tripping”. In the first case, a fault detection via mains fuse is not possible in every situation, because of the penetration with DGs the SCC though mains fuse can be less than minimum tripping current. In the second case, the fault can be mistakenly detected in a wrong feeder, because of DGs contribution to SCC. To avoid such effects, a permanent tracing of current at relevant nodes can be a solution.

### RVK Simulator
In the [n5geh.services.rvk_simulator](https://github.com/N5GEH/n5geh.services.rvk_simulator/tree/master), the simmulation of different modes is possible.
This use case represents a comprehensive control structure in the scope of the "Regional Virtual Power Plant” (RVPP).
The structure of power generation will move from the current hierarchical and centralized architecture to a more decentralized one, which is also driven by the increasing integration of renewable energy sources. Regarding this, the main objective of the use case is to improve the balancing of energy generation and energy consumption in a local district by using intelligent regional networks. Hence, this approach also leads to a reduction of the load of transmission grids. Furthermore, it is possible to participate in the energy market and generate revenue by bundling several systems and the ability to respond quickly. In addition to the higher level control tasks, the use case generally also contains control tasks of the local energy system. This control can be carried out with several objectives, such as the reduction of energy costs or an increase in the portion of own consumption of renewable energies. In order to achieve the central objectives described above, the fulfilment of subtasks is required. This includes the prediction of the thermal and electrical load which is a significant part of the creation of an energy trend band. The energy trend band contains the prediction of the energetic flexibility of the system, and thus defines the potential for a positive or negative load shift. 

## Devices
### IoT-DIO Digital IO IoT Wireless Adapter
IoT-DIO is a wireless adapter for developing IoT applications for industrial and building automation systems based on the Espressif chipset ESP32. The device can be reached through [n5geh.devices.iot_wa_dio-](https://github.com/N5GEH/n5geh.devices.iot_wa_dio-).

### IoT-AIO Analog IO IoT Wireless Adapter
IoT-AIO is a wireless adapter for developing IoT applications for industrial and building automation systems based on the Espressif chipset ESP32. The device can be reached through [n5geh.devices.iot_wa_aio](https://github.com/N5GEH/n5geh.devices.iot_wa_aio).

# Acknowledgments
We gratefully acknowledge the financial support of the Federal Ministry
for Economic Affairs and Climate Action (BMWK), promotional references 
03ET1561A, 03ET1561B, 03EN1030B, 03EN1030A

<a href="https://www.bmwi.de/Navigation/EN/Home/home.html"> <img alt="BMWK" 
src="https://raw.githubusercontent.com/RWTH-EBC/FiLiP/master/docs/logos/bmwi_logo_en.png" height="100"> </a>
