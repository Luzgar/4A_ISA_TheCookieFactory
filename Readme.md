# The Cookie Factory (ISA Case study)

  * Author: Sébastien Mosser [mosser@i3s.unice.fr](mosser@i3s.unice.fr)
  * Reviewer: Anne-Marie Déry [pinna@polytech.unice.fr](pinna@polytech.unice.fr)
  * Version: 02.2016

This case study is used to illustrate the different technologies involved in the _Introduction to Software Architecture_  course given at Polytech Nice - Sophia Antipolis at the graduate level. This demonstration code requires the following software to run properly:

  * Build & J2E environment configuration: Maven 3
  * J2E implementation language: Java 8
  * .Net implementation language: Mono >3.12


## Product vision

_The Cookie Factory_ (TCF) is a major bakery brand in the USA. The _Cookie on Demand_ (CoD) system is an innovative service offered by TCF to its customer. They can order cookies online thanks to an application, and select when they'll pick-up their order in a given shop. The CoD system ensures to TCF's happy customers that they'll always retrieve their pre-paid warm cookies on time.

## Chapters

  1. Architecture
  2. Business components with EJB Sessions
  3. Exposing components as Web Services (SOAP)
  4. Consuming external Web Services (REST)
  5. Unit testing _versus_ Integration testing
  6. Complete architecture overview
  7. Message interceptors to support the NTUI (_Never Trust User Input_) golden rule 
  8. Making things persistent
  9. Conclusions

__Important remark__: one can notice that the persistence layer (_aka_ the database) is the last step of this document. This is done on purpose. Databases are part of a given architecture, but must not be considered as the its essence. The essence of an architecture is the set of supported features, at the business level. Databases are in this context only a way (among others) to store data.

## How to use this repository
  
  * The `develop` branch (the default one) represents the system under development. 
    * The [`releases/1.0`](https://github.com/polytechnice-si/4A_ISA_TheCookieFactory/tree/release/v1.0) branch contains the code that implements the system without persistence
    * The [`releases/2.0`](https://github.com/polytechnice-si/4A_ISA_TheCookieFactory/tree/release/v2.0) branch contains the code that implements the system with a real persistence layer
  * Issues can be submitted using the GitHub ticketing system

### Compilation & Execution

To compile the demonstration (j2e, .Net and client parts), simply run the compilation script. The first compilation can take (a lot of) time, considering that Maven will have to download all the java dependencies necessary to build and run the system (the application server weights 43Mb):

    mosser@azrael $ ./buildAll.sh
    
To run the demonstration, first start the two servers in two different terminals, then start the remote client in a third one:

    # J2E terminal 						(^C to stop)
    mosser@azrael $ cd j2e
    mosser@azrael j2e$ mvn tomee:run
  
    # .Net terminal						(return to stop)
    mosser@azrael $ cd dotNet
    mosser@azrael dotNet$ mono server.exe
    
    # Remote Client						(bye to stop)
    mosser@azrael $ cd client
    mosser@azrael client$ mvn exec:java