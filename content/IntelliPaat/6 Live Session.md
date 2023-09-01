
![[Pasted image 20230806112311.png]]

[[Software Development]] is the process of transforming customer requirements into a complete software product. ([[SDLC]])

Requirements 
  This is the most important phase in the software development lifecycle. In this stage, the requirements are gathered from the customers and the requirements are then analyzed to ensure their feasibility.
Design
  Once the requirements are received, the architect transforms these requirements into technical specifications and plan the software components which have to be designed
Implementation
  The specifications are then passed on to the developers which create the application based on these specifications

Verification - make sure that it does what is meant to
  Once the development work is done on the application. It is verified by a group of testers to map the application's functionalities with the specification given by customers. QA

Maintenance
  Once the code is verified, it is pushed to production. Post this, the application is updated with any future enhancements or optimizations, if and when required.



Since the time software development started, various software development models have been curated which implement [[SDLC]]. Each of these models solve problems that existed before these models were invented.

Traditionally, there have been 3 major [[software development models]] that most companies follow:
  [[Waterfall Model]]
  [[Agile Model]]
  [[Lean Model]] 


![[Waterfall vs Agile vs Lean.png]]


## Why DevOps

Although, the software quality was improved. We still had a lack of efficiency among the development team. A typical software development team consists of Developers and Operations employees. Let us understand their job roles

Developer
A developer's job is to develop applications and pass his code to the operations team

Operations
The operations team job is to test the code, and provide feedback to developers in case of bugs. If all goes well, the operations team uploads the code to the build servers

Conflicts or roles/responsabilities
The developer used to run the code on his system, and then forward it to operations team.

The operations when tried to run the code on their system, it did not run!

This led to a lot of back and forth between the developer and the operations team, hence impacted efficiency.

This problem was solved using Devops!


## Traditional IT vs DevOps

Traditional IT:
Less Productive
Skill Centric Team
More Time invested in planning
Difficult to achieve target or goal

Devops:
More Productive
Team is divided into specialized silos
Smaller and Frequent releases lead to easy scheduling and less time in planning
Frequent releases, with continuous feedback makes achieving targets easy

## What is DevOps?

Devops is a software development methodology which improves the collaboration between developers and operations team using various automation tools. These automation tools are implemented using various stages which are a part of the Devops Lifecycle


## How DevOps Works?

The Devops Lifecycle divides the SDLC lifecycle into the following stages:

Devops build systems that do or enable continuous development

Things happens in parallel to ensure availability for everybody

#canvas
![[How DevOps Works.png]]

![[How DevOps Works2.png.png]]


Continuous Development
This stage involves committing code to version control tools such as Git or [[SVN]] for maintaining the different versions of the code, and tools like Ant, Maven, Gradle for building/ packaging the code into an executable file that can be forwarded to the QAs for testing.

Continuous Integration
The stage is a critical point in the whole Devops Lifecycle. It deals with integrating the different stages of the devops lifecycle, and is therefore the key in automating the whole Devops Process

Continuous Deployment
In this stage the code is built, the environment or the application is containerized and is pushed on to the desired server. The key processes in this stage are [[Configuration Management]], [[Virtualization]] and [[Containerization]]

Continuous Testing
The stage deals with automated testing of the application pushed by the developer. If there is an error, the message is sent back to the integration tool, this tool in turn notifies the developer of the error. If the test was a success, the message is sent to Integration tool which pushes the build on the production server

Continuous Monitoring
The stage continuously monitors the deployed application for bugs or crashes. It can also be setup to collect user feedback. The collected data is then sent to the developers to improve the application

## DevOps Tools
We have discussed the Devops Methodology, but this methodology cannot be put into action without it's corresponding tools. Let us discuss the devops tools with their respective lifecycle stages


