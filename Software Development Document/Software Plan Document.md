# Software Plan Document

__Project Moosic__

Author: JeremyCJM

# 1. Overview

## 1.1 Project Summary

The goal of this project is to develop a web-based music player that can play specific music that matches users’ mood. The documents will be released at the same time.
Milestones include the releasing of Software Requirement Specification, Software Management Plan, Software Design Description. The whole estimated develop period is 15 weeks.

##1.2 Product Delivery

The delivery date is June 1. Delivery content mainly include executable server program and server code, a set of executable web applications and web application source code, a complete set of technical documentation, including requirements specifications, system design specifications and other software documentation.

##1.3 Timeline

a. Before April 25, 2019
Complete investigating and researching works, summarize concrete requirements. Realize the fundamental UI
b. Before May 25, 2019
Add the face emotion recognition, music emotion recognition module and recommendation module. 
c. Before June 8, 2019
Final function and UI refinement. Complete testing. 

# 2. Project Organization

## 1.1 Internal Structure
Democratic organizational structure, the decisions in the development are made through discussing of all members. The code uploaded to the GitHub must be checked by another member. The tasks will be allocated according to the coding skill levels and project experiences, so that the scenario of imbalance of workload would not happen.

## 1.2 External Interfaces

Organizations|Contacts|Contact Info
:-----------:|:------:|:----------:
Instructor|Teacher Wu|wuchxcourse@sina.com
QA|JeremyCJM|2673001732@qq.com
Principal|Touko|touko@whu.edu.cn

## 1.3 Roles and Responsibilities

Role|Responsibility|Person
:--:|:------------:|:----:
Product Manager|Requirements analysis, software architecture design|Touko
Developer|Concrete functions realization|Kyrie, JeremyCJM
Tester|Code testing, software quality assurace|Colorofnight

# 3. Management Process Plan

## 3.1 Start-up Plan

Each member of the team can make their own opinions regardless of their role, and all members of the team will decide whether to adopt them. Decisions need to be approved by the team members before they can be implemented. After the decision is made, it should be supervised by relevant personnel to ensure that the decision can be completed sooner after the decision is made. The progress of the team development should be completed as soon as possible, and the test progress of the product should also be carried out on time. Products should follow the proposed specifications and be carried out in strict accordance with pre-set documentation. The project code is readable so that they are easy to maintain. The project should run steadily and have good user interaction. The project should try to meet the needs of music lovers and provide music lovers with a good platform for music management and daily use.

## 3.2 Work Plan

1~6 week：Finish the SRS and SPMP documents
7~10 week：Finish the Architecture Designment and SDD document
11~13 week：Finish testing
14~15 week：Finish the software delivery and write the summary document
## 3.3 Control Plan

The person in charge of each development process records the progress of the work on a half-month basis, forms an electronic document report, and uploads it to the document library. The person in charge will make an online summary at the weekly meeting, and the other members will give their opinions through the review, and the report will be uploaded to the document library after modification. The risk leader closely monitors the risk status, submits a risk report on a regular basis, and notifies all team members of the emergency mailing list if necessary, and the team leader makes a temporary decision. At the weekly meeting, the group discussion will be adopted after the consensus is reached. The relevant responsible person will carry out the next week's work on the improvement opinions, and the group meeting will continue to evaluate its effectiveness. Before the end of each project phase (before and after the milestone), organize a phase review meeting to assess the efficiency and quality of the results throughout the phase. Try to merge with the regular meeting of the project and invite teachers and QA to participate in the review.

## 3.4 Risk Management Plan

Risk ID|Risk|Probability|Impact|Priority|Mitigating|principal|Expected Date
:-----:|:--:|:---------:|-----:|:------:|:--------:|:-------:|:-----------:
1|Development skill is not mature|60%|disaster|high	Develop a study plan in advance;Reduce design difficulty|Touko|Before 8th week
2|Facial emotion recognition model has low accuracy|70%|serious|high|Test the machine learning model with new data, add new data for training if necessary, adjust parameters appropriately, and take care to prevent overfitting|JeremyCJM,Kyrie|Before 9th week
3|Training time is too long|70%|serious|high|Be careful to use vector operations when writing neural network models; use a computer with GPU for training|JeremyCJM|10th week
4|The player cannot play the music fluently|60%|serious|high|Research on streaming media loading, preloading and caching in advance|Touko,Kyrie|12th week
5|Frequent demand changes|50%|serious|medium|Demand development fully foresaw the future;More communication with the QA group;Design plan leaves room for change|Colorofnight|8th week
6|Lack of design talent|50%|medium|high|The team members have in-depth study of relevant knowledge; Seeking foreign aid to help|Colorofnight|10th week

A detailed description of the risks is as follows:
- Risk 1: Unskilled development techniques
Some of the team members did not use django for background development experience before, which may slow down the progress of the project.
- Risk 2: The facial emotion recognition model has low accuracy
Using existing facial emotion recognition machine learning models may be over-fitting to the original training data set, which may result in low recognition accuracy of new data in actual use.
- Risk 3: Training the neural network model for too long
Because of the many parameters of the neural network, if the programming is improper or the CPU is used for training, the training time may be too long.
- Risk 4: Web music player can't play smoothly
The web music player may be stuck or unable to play because there is no technical processing such as preloading.
- Risk 5: frequent changes in demand
During the design and development process, it may be found that the original requirements are not easily converted into design drafts. During the test experience, it may be found that the game is not fun, which will bring about a new change in demand. In both cases, especially the latter one should be avoided as much as possible to avoid waste of repeated development.
- Risk 6: Lack of design talent
Design is very important for a piece of software, but there is no such talent in the project team, which may lead to a decline in product appeal and more time spent on interface development.

##3.5 Project Close-out Plan

After the development is over, the team will invite some trial users and QA teams to test. This part of the user will not know the specifics of the requirements document and maximize the simulation of future users' use of the software. This part of the user will submit feedback to the in-group test docker to confirm whether the requirements document and test document need to be updated and update the project code. At the same time, a small number of people inside and outside the group will be invited to perform software testing based on the test documents to improve the stability and accuracy of the software. After the above tests are completed, write the software delivery documentation and supporting documentation and deliver them.

# 4. Technical Process Plans

## 4.1 Process Model

Applying the prototype model, first establish a preliminary prototype of the system, compared to the actual software, usually only limited functionality, low reliability and imperfect system structure. Then, using an additional strategy, by providing users with feedback on the prototype acquisition, the deficiencies of the prototype are gradually supplemented, and the software is perfected. Since the opinions of users and developers are basically agreed throughout the development process, the developed software meets the user's expectations and can also reduce design errors and hidden risks during the development process.

## 4.2 Method, Tools and Technology

The group is mainly composed of programmers. The programmer completes the documentation and testing work while taking on the coding task. The programming languages are mainly Python, JavaScript (NodeJS), TypeScript, CSS, Less, HTML, SQL, mainly using object-oriented design methods. The construction of models, data streams, etc. is done by StarUML software. Document writing is done by Google Document, Microsoft Word, and Markdown.
The developer completes the unit test writing at the same time as the code. The software code update uses a mutual audit system, that is, when any programmer submits the code, one or more other team members must agree to the code update request before the code can be merged. If there is a problem with this part of the code, the writer and the reviewer share responsibility.

## 4.3 Fundamental Infrastructure

Personal Computer, server

## 4.4 Quality Control Plan

Team members should do their best to design and produce products based on requirements documents. At the same time, the group should conduct phased review work, regularly check the modules with problems and modify them in time.

## 4.5 Project Improvement Plan

Based on the completion of the basic functions, the project documentation and coding content can be improved through the agreement of the team members and the customer. When problems arise, you can perform root cause analysis on recurring problems, implement project improvement plans, improve project quality based on existing projects, and correct problems in the project that are different from customer needs.

# 5. Supporting Process Plans

## 5.1 Inner Support

//TODO 这个表要怎么画

## 5.2 Testing Plan

### 5.2.1 Scope of Testing

#### 5.2.1.1 Features to be tested

Module Name|Description|Tester
:---------:|:---------:|:----:
Music Player|The music player should be able to play fluently and pause or resume a music|Colorofnight
Face emotion recognition|The emotion of a user should be accurately recognized|Kyrie
Music emotion classification|The emotion of a music should be accurately classified|JeremyCJM
Matching the emotion of music with user’s mood|The emotion of music should be matched with the emotion of user|Colorofnight
Music Management|Users should be able to manage their own music, including uploading, downloading and deleting, and can set the music as a favorite, create a song list and add songs to the song list|Touko
Music community|Users should be able to post their own comments under each song and share song links to their like-minded friends|Touko


#### 5.2.1.2 Features not to be tested

These features are not be tested because they are not included in the software requirement
specs
- Hardware interfaces
- Database logical
- Website Security and Performance

### 5.2.1 Test Type
In the project Moosic, there are 3 types of testing should be conducted.
- Integration Testing (Individual software modules are combined and tested as a group)
- System Testing: Conducted on a complete, integrated system to evaluate the system's compliance with its specified requirements
- API testing: Test all the APIs create for the software under tested

## 5.3 Source Support

- Personnel: Developer, Customer, QA Team
- Software: Code Development IDE, Chrome, Document Authoring Tools, etc.
- Hardware: PC, server
- Working environment: dormitory, library, classroom
- Other: Because this project involves deep learning, a high-performance computer capable of training a large number of data sample models is needed. Later, we will consider using the Wuhan University Supercomputing Center for sample training.

## 5.4 Budget and Resource Allocation

The project does not need to consider budget and resource allocation for the time being.

## 5.5 Theoretical Support

Due to the content of machine learning and deep learning, this project requires team members to have a certain understanding of cutting-edge machine learning and deep learning and can quickly search for the required machine learning or deep learning theory from existing open journals and conferences. And verify its availability in this project.
