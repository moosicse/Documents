# Software Design Document

__Project Moosic__

Author: 



# 1. Introduction

## 1.1 Purpose

This is a design document of the Project *Moosic*. This is a music player project that incorporates the ability to filter songs based on user mood. For information related to this project, please refer to the software requirements document. 

The intended readers of this manual are system designers, software developers, software testers, and project reviewers (QA Team).

## 1.2 Scope

This document defines the design portion of the software. The document includes software module design, internal interface design, data storage design, data flow design, external interface design, user interface design, algorithm and process logic, and so on, providing the basis for the normal development of software and system maintenance.

## 1.3 Definition and Acronyms 

No content yet.

# 2. References 

- Django - <https://docs.djangoproject.com/en/2.2/>
- Django Rest Framework <https://www.django-rest-framework.org/>
- React - <https://reactjs.org/>
- Mobx - <https://mobx.js.org/>
- Ant Design - <https://ant.design/>

# 3. Software Architecture

## 3.1 Internal Architecture

### 3.1.2 Brief Introduction

The Moosic project uses MVC's software architecture. It layers data, views, and controllers to ensure that the software is loosely coupled in the vertical direction. Part M (Model) is focused on data processing, Part V (View) is responsible for software interface rendering, user interface and user interaction, and Part C (Controller) is responsible for data processing and connecting parts M and V .

### 3.1.2 Design Concept

We believe that the loose coupling of software must be defined from the beginning of software design, so we have specified MVC as the internal architecture of our project. 

#### Model

As mentioned above, Part M is responsible for processing the data. Engineering data storage and invocation is solely the responsibility of Part M. Part M specifies the structure of the database, designing and storing engineering data in an object-oriented manner, and providing complete interface calls. The way the database is invoked is not called in the previous SQL Query mode, but in the way of ORM. This fits the code style of the object-oriented language we use (Python), and it also provides better maintenance complexity and lower coupling.

#### View

Part V is responsible for user interaction. It narrowly refers to the user interface in this project. The user interface is rendered by the browser, and logical operations are implemented through the API of the backend package, ultimately resulting in a complete user interaction process. The Part V performs only a few simple logical operations and does not perform more complicated logic processing. More difficult database operations or data filtering operations are handled by the backend. The main role of the Part V is to present the information sent from the backend to the user. The backend here is the Part C, which will be described below.

#### Controller

Part C is the part of this project. It reads and filters information from the M part (database), processes the data, and then sends the filtered data to the V part. It contains the following basic functions:

- Part C needs to pass the serialization module to strictly control the data to ensure that the least amount of data is returned.
- Part C needs to avoid unauthorized reading and writing of data.
- Part C is the last line of defense for incoming data to prevent malicious data injection from damaging the system.

So this is a module that needs the most careful consideration.
We first deprecated the way Django's own Template rendering methods and completely separating the project to frontend and backend architecture. They only correlating through data communication. This can make the program loose and easy to develop. At the same time reduce the pressure on the server, the page rendering is done by the user's browser. This may result in a bad experience for some users with lower configurations, but it can be ignored.
Second, in the MVC architecture, the Controller is the part we need most unit testing. We have defined the development plan for unit testing. Considering that the Part Model has a very low failure rate due to the commonly used framework, there is no need to write unit tests. Due to the particularity of the browser's work, the Part View must ensure that its code logic is reliable, and most of the problems that arise are Part Controller's problems, and there is no need for unit testing. Unit testing is very important in the controller that connects the above.
Therefore, we divide the Controller into two parts, one is the Views part of the Django framework, and the other is the Services section we specify. Views provides backend rendering in the original Django framework. But in this project, the Views section will focus on the packaging of the API. Thanks to the good interface and reliable packaging provided by Django-Rest-Framework, Views can be efficiently designed as CURD. But why do we have to be a separate service? Considering the coupling of the code and the possible reuse, it is a wise choice to separate some of the general logic or complex logic into Services. This design can provide a better Debug environment for subsequent development.

## 3.2 External Architecture



# 4. Decomposition Description 

## 4.1 Module Decomposition 

### 4.1.1 Module Music 

#### Overview

Module Music is the most important module of this project. It provides a fully controller of music in one website. Music's information is stored here, working together with the music's service and views to provide the operation for both user and staff.

#### Scope

Module Music mainly stores music-related data in a narrow range, such as the song's name, song files, foreign keys of a singer and so forth. The music module does not process other related information, such as albums, singers, this part of the information is stored by the extra module, and only the foreign keys are processed in the music module. 

Module Music contains one of the most significant service of this project - mood recognition service. Although the mood recognition module is not a separate module, it needs to be a separate service and belongs to the Module Music. To get a brief description and detailed design information, please refer to the [7.3 Service Detailed Design](#7.3 Service Detailed Design).    

TODO: Finish this hash tag link. 

### 4.1.2 Module User

## 4.2 Business Process Decomposition

Here are a decomposition of several business processes that will be widely used. 

### 4.2.1 Business Play Music

#### Entry

#### Internal Process

#### External Process

#### Export

# 5 Dependency Description

## 5.1 Backend Dependency

## 5.2 Frontend Dependency

## 5.3 Database Dependency

## 5.4 Automatic Build Dependency

# 6 Interface and Service Description

## 6.1 User Interface Description

## 6.2 Internal Interface Description

## 6.3 Service Description

# 7 Detailed Design

## 7.1 Module Detailed Design

### 7.1.1 Module Music

#### Module Permission Control

## 7.2 Interface Detailed Design

## 7.3 Service Detailed Design













