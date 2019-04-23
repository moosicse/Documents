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













