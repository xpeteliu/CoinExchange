# CoinExchange, by Xinyue (Pete) Liu

### Description
This project was originally maintained in a private Gitee repo, and then forked here after completion. My backend work for the online crypto exchange is located in the directory */coin-exchange*. The folder *coinexchange-ui* contains its corresponding frontend codes, which were not created by me (but I modified part of them to add support for Websocket and STOMP requests).

### File Structure
This backend project tries to follow the microservice architecture and the Domain-Driven Design pattern. Each subfolder in */coin-exchange* contains a microservice of its own (except for *ce-common*, which serves as a common dependency for other modules to provide helper functions). These modules can be run on different server machines. Inside each module, folders named like *\*-api* contain the interfaces for the Remote Procedure Calls across modules and probably other supporting codes pertaining to RPC (e.g., definitions of Data Transfer Objects). In this project, the RPCs are implemented via OpenFeign, and the FeignClient instances are also defined in the *"\*-api"* folders. 

Other folders contain the main business logics. For example, *authorization-server* contains the codes for the Auth Server which is responsible for authenticating users and issuing tokens, and *channel-service* includes the functionality of instantaneously publishing price updates and other information to the channels subscribed by the client. Most of the folder names are self-explanatory, and one may check the Maven POM files to see the frameworks used in these services. Inside a business-logic folder, the subfolder *controller* / *service* / *repository* corresponds to the controller / service / persistence layer respectively. The subfolder *model* defines View Objects which are sent as response bodies to the frontend, and the subfolder *entity* defines Persistence Objects which are stored as records in the relational database. I mainly used Spring Data JPA (and occasionally, Spring Data JDBC) to interact with the MySQL Database.
