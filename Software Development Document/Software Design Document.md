# Software Design Document

__Project Moosic__

Author: Touko

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

### 3.1.1 Brief Introduction

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

### 3.1.1 Brief Introduction

As mentioned above, we will use a separate architecture at the frontend and backend, with the connection of database located at the side of backend. A more detailed description of the external architecture of this program is provided below.

### 3.1.2 Design Concept

The program will be divided into frontend and backend for development. The frontend and backend are each placed in different code repositories, using different languages but sharing the same set of APIs and data structures. 

#### Frontend Internal Structure

When the user opens the browser and accesses our web page, the browser's URL will be forwarded to index.html. This logic is implemented by Nginx. The first thing that is presented to the user is the layout of the frontend. Layout includes Header, Footer, Navigator (Menu) and Content. The Content section will be routed by the URL to distribute the user to different pages.
The frontend will be divided into modules. There is a route inside each module to control the routing of pages within the module. Software frontend routing will be structured as follows. The global route first directs the user to a different module based on the URL matching result. The intra-module routes are then matched to provide user interaction and other related services.

#### Frontend External Structure

To get a compact and scalable structure, we use Nginx as the web server program. It provides two basic function: Web Server and Reverse Proxy Server. Nginx will open a web access port to the frontend page after the compilation and build, and provide access to the user's frontend web page. At the same time, the backend Django will be reverse proxyed. The purpose of this is to prevent browsers from cross origin errors and providing users with secure web access. 

#### Backend Structure

The backend provides API services to frontend web pages through Nginx's reverse proxy. The backend is also divided into modules. The module takes Model as the core and provides API through Views and Services in the Controller layer. At the same time, parts such as event triggers, global constants, and timing parallel tasks may exist in the module at the same time. The module was previously associated with the global settings file, using Django's own routing for access control between different APIs.

The backend currently uses the SQLite3 database. As a start-up project, the database pressure is not large, so there is no need to use a commercial high-concurrency high-stress database. The program's music files are allowed to be stored in multiple sources. The current server, third-party storage repository or CDN can be used as the storage location for static music files. The cache uses the native memory cache. It is expected that the larger cache will not be used at present, and there is no need to worry about cache hot swap.

## 3.3 Source Code Architecture

### 3.3.1 Frontend Source Code Architecture

### 3.3.2 Backend Source Code Architecture

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

#### Overview

The Module User is used to store all user-related information, including user attributes, permissions, and so on. The Module User has a one-to-one correspondence with the users provided by Django's own Authentication module, which facilitates user login and session permission control.

#### Scope

The Module User stores user-related information. Whether the user is a Staff or Super Administrator is set and executed by the Django Authentication module. Some songs require permission control, and the Module User can set a permission group Model separately. When the song needs permission control, the user is added to the permission group, and the song is set to the permission, so that the authority can control the song. Doing so allows users to privately upload songs or share songs in small circles.

User preferences and recent mood information will also be stored in the Module User. This allows the program to better push songs or filter songs for the user, allowing the program to do smarter things.

## 4.2 Business Process Decomposition

Here are a decomposition of several business processes that will be widely used. 

### 4.2.1 Business Play Music

#### Entry

The most important function of the music player is to play music, so the music playing business will be the most frequent and most reliable business. The user may play music at any time, such as searching for a song and clicking on the search result, clicking on the song in the album, clicking on the song on the artist page, playing a song on the radio or song list, triggers the music playing music.

#### Process

When the user initiates a song request, the program passes a music id. The program will find the corresponding song based on this id and return music information and binary streaming media files. After the browser receives the relevant information, it provides the user with browser-level music playback. 

As mentioned above, the storage location of the music streaming media file can be arbitrary. In the case of initial service operations, music files can be placed in a public folder and stored in a database. Provide the interface to the user when the user needs it. If it is stored in the CDN, when the music is uploaded, the music file is directly transmitted to the CDN, and the resource address corresponding to the CDN is recorded. In this case, when the user acquires music, the program first confirms the user's authority on the music file. If the user is allowed to access the music file, the system will provide a temporary token to the user, allowing the user to obtain the streaming file directly from the CDN.

### 4.2.2 Business Next Song With Mood Recognition

#### Entry

One of the biggest differences between our project and the traditional music player is that it will randomly play and filter the music according to the user's mood. This service will be activated when the user turns on the song according to the mood and performs music switching.

#### Process

In order to complete this set of services, we must first model the mood based on each song. We use the pre-trained neural network to judge the mood of the song according to the tune, rhythm, lyrics and other information of the song, and score the song in several mood dimensions and store it in the song information. The use of pre-trained neural networks is due to the problem of server performance. It is not possible to run a stressful model on the server. It is necessary to use additional computational power for model training.

After the modeling is completed and the music mood score is given, we need to establish a mood transition state map of human maximum probability based on the existing research to provide services for the subsequent operations. The purpose of this is to recommend the most suitable music by the user's current mood, the ultimate goal is to keep the user in a better mood state. We consider a variety of ways to get user mood, such as face recognition, arm swing frequency, heart rate and so on. Considering the limitation of system calls, we currently only consider the way of face recognition to get the user's mood. Here again a new neural network is needed.

The neural network is based on existing facial recognition methods and provides a multi-dimensional user facial expression scoring, such as happiness, sadness, anger, and the like. The model needs to be as lean as possible and able to judge the user's mood faster. In the business process, we first ask the user to agree to take the user's face image, then judge the user's mood, and finally recommend the song according to the recommendation method described above.

# 5 Dependency Description

Only important program dependencies will be introduced here.

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













