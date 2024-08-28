+++
title = 'From Software Engineering to Cybersecurity: My Journey So Far'
date = 2024-08-20T08:53:41-05:00
tags = ['career']
draft = true
+++

Hello! I'm a software engineer with a deep passion for technology that started at a very young age. 

I was born and raised in Portugal, where my curiosity for technology and computers began. I was always fascinated by how things worked. This fascination eventually led me to pursue a degree in Computer Science in Lisbon.

From an early age, I was drawn to programming. I have fond memories of exploring on an old Windows 95 computer and experimenting with microcontrollers. My father played a significant role in nurturing my interests, giving me a book on C programming when I wanted to learn how to control LEDs with microcontrollers. This early exposure to technology set the foundation for my future career as a software engineer.

Though my career has been rooted in software engineering, my interest in cybersecurity has been present since my teenage years. While there weren't many opportunities in this field in Portugal early on, I've always stayed curious and informed. Now, as I take a break and shift gears, I'm diving into cybersecurity with the goal of integrating it into my work with web technologies.

This journey from software engineering to cybersecurity feels like a natural extension of my curiosity and passion for technology, as I continue to explore and innovate in new areas.

## My Academia Path

In 2009, I embarked on my academic journey in Computer Engineering, which culminated in earning a master’s degree in 2015. Throughout my time at university, I developed a strong affinity for various subjects, particularly those that challenged my understanding of systems, programming languages, and security. 

I had to work on a diverse range of projects, predominantly using Java (SE 6 and SE 7), but also exploring other languages like C, C++, HTML, CSS, JavaScript, OCaml, Objective-C, and Prolog. My passion for learning about different technologies and topics was a driving force throughout my academic career.

During my studies, the courses I enjoyed the most were:

- Concurrency and Parallelism: In this course, we were tasked with analyzing a 10GB dump of Twitter data. Using Apache Storm, I processed the tweets to identify the top 10 users with the most tweets, utilizing georeferenced data. By mapping these tweets, I was able to infer the workplaces, gyms, and even the residences of these individuals—a project that deepened my understanding of big data processing and real-time analytics.

- Computer Networks: One of the most fascinating experiences was learning about and configuring protocols like TCP, UDP, DNS, BGP, and RIP on Cisco routers in a lab environment. This hands-on experience provided me with a solid foundation in understanding the stack of protocols that continue to underpin the internet today.

- Artificial Intelligence: This course introduced me to the core concepts behind neural networks, laying the groundwork for understanding the deep learning models that have become so prevalent in today’s AI landscape.

- Data Warehousing (SAIA Project): In this project, we analyzed student bidding and university results data to predict the number of openings the university should offer for the next year. This project enhanced my skills in data analysis and predictive modeling.

- Integrative Project: For my capstone project, I developed the winning application in my class—a management system for scientific conferences. The app, implemented in Objective-C for iOS 6 on the iPad, managed key speakers, regular speakers, rooms, booths, and participants, showcasing my ability to design and implement comprehensive solutions.

- Master’s Dissertation: My dissertation focused on database performance, specifically testing the Non-Monotonic Snapshot Isolation (NMSI) algorithm as a potential replacement for Snapshot Isolation (SI) in traditional databases. The goal was to evaluate whether NMSI could maintain the same ACID guarantees while improving performance—a study that deepened my expertise in database systems and transactional consistency.

My academic journey provided me with a solid foundation in computer engineering, equipping me with the skills and knowledge to tackle complex problems and explore diverse areas within the field. These experiences have been instrumental in shaping my professional path.


## My Professional Path

My professional journey began during my time at university, where I worked as an assistant professor. This role involved teaching and helping students from various engineering disciplines learn the basics of programming. It was an unique experience that deepened my understanding of programming concepts and refined my ability to break down complex ideas into simpler parts.

In 2015, I worked on a freelance project with Global Change Fluxphera, a company focused on process improvement, implementation, and change management through systems and learning processes. I led the development and deployment of a collaborative virtual real-time web game designed to positively influence organizational behavior. This project involved working with *Node.js*, setting up virtual machines on *AWS*, and configuring *Docker* containers to ensure seamless execution of all parts. It was a six-month project that not only enhanced my technical skills but also taught me the importance of adaptability and delivering tailored solutions that meet client specifications.

Following this project, I joined Sqimi in 2016, a consulting company where I started working with *OutSystems*, a low-code platform for web developement. Although low-code and web development weren't my first choices, I quickly adapted to the evolving industry trends, focusing on web technologies.
Here I joined a project about maintaining and developing various aspects of a custom Customer Relationship Management (CRM) system, particularly focusing on customer services at stores for a Highway Toll Company.  

One of the most significant challenges I faced on this project was splitting and migrating the on-premise infrastructure to a cloud service. This task involved splitting the internal *Oralce* database schema into parts, syncing a subset of the datamodel to the cloud for customer-facing applications and ensuring seamless functionality for both internal processes and customer-facing applications. 

In 2019, I joined IG&H, where I participated on diverse challenges and projects that further expanded my expertise, with contributions across multiple domains, including pension solutions, travel agency digitalization, research and development, and performance evaluation systems.

One of my early projects was on health to support Diabeter patients, where I played a key role in developing the first iteration of platform for diabetic patients to track and share their health data. This application allowed healthcare professionals to monitor patients’ values, medication, and overall well-being, shifting the focus of healthcare from reactive to proactive.

Then I joined a project in the pension domain where, in the Factory Team, I contributed to the transition from an old system to a new core system for managing pension funds. Despite the challenges, including obtaining detailed requirements from the business side, it involved migration the data from another *Oracle* database to *SQL Server* to be able support Outsystems development of more teams, build a CI/CD pipeline in *Jenkins* and incorporation it into the Outsystems tooling, *Lifetime*, to trigger the acceptance tests and the deployment of code to another environment 
and multiple AWS for various functionalities, setting up *AWS SQS* to share workitens between different services, AWS SNS Topic for event notification, configuring AWS S3 buckets to receive file from third parties, and monitoring all the services used with CloudWatch.
This project was a critical learning experience in understanding the importance of clear communication between technical and business teams.

In 2021, I joined the Research & Development team, where I worked on innovative projects that pushed the boundaries of low-code software development. In this team, one of ours responsabilities was to support other teams, specially if ti envolve other tecnologies outside of Outsystems, for example I developed the integration of a Azure Active Directory and helped with the integration of other SAML provider into Outsystems. Including other cloud services and solution in the Outsystems enviroment proving the developer with newer services, for example implementing an api management solutionswith *Azure API Management*, setting up *SignalR*. 

Although a lot of our focus was still development regarding research one of the highlights was my involvement in a project, where we built a virtual engagement agent with gamification elements for employees. This project allowed me to explore the intersection of technology and human behavior, as we developed a system where employees could set and achieve personal KPIs in a gamified environment. We utilized *Azure Cloud* services, including *message queues* and *Azure Functions*, and explored *Azure Cosmos* for database. The project also involved implementing *SignalR* for real-time communication and notifications, ensuring seamless interaction between different system components.

In this team, as the lead developer in Outsystems, I spearheaded the design and implementation of a Performance Evaluation App for the company. The app featured a microservices architecture of feedback system encouraging a culture of continuous improvement, a goal management component enabling employees to set and track their professional objectives, a mentor application enhancing mentor-mentee relationships through feedback and goal monitoring, and an evaluation tool that streamlined the evaluation process through collaborative assessments and detailed KPI analysis. Being a microservices architecture each system had an independent database so syncronization was very important, we notified key events to other systems through *Azure Event Bus* and the source of true database was implemented like a graph database with nodes and relations (edges) in order to be schemeless and future proof to changes of the data represented, although we could used *Azure Cosmos DB* for Apache Gremlin, this pattern was implemented over the Outsystems database *SQL Server*.

In 2023, I led the digitalization project for a travel agency, integrating OutSystems, OpenRPA and AI for improvement of customer support and integration with Zendesk. In this project we used Outsystems as an integration point between the old CRM and a workforce of robots in OpenRPA to improve and automate processes of notification of the customer, like sending the details of flights, hotels or register customer support interactions on the CRM.
This project was particularly exciting as it also involved leveraging artificial intelligence, OpenAI GPT-3, to streamline the interpretation and extraction of flight change information from emails. The result was a dynamic customer support system that significantly improved efficiency and accuracy within the customer support workflow.

Later this year, I participated on the *Healthcare Hackathon* in Mainz, German. The main objective of this event was to "Rethinking health" with interdisciplinary teams of doctors, nurses, experts, employees and patients working together on creative solutions for the healthcare of tomorrow. As one of the key developers, we presented a transformation tool to disrupt the backoffice process of acquire medical equipment for the clinics leveraging Outsystems and Docusign. This tool provided the clinics with a streamline acquisition process allowing for approval of the different stakeholders using digital signatures from the first request to the creation of the formal contract with the supplier. In the end we won the First Price of the this competition, Outsystem really excel in this context to go from zero to a POC in a very few hours.

On the last project I participated we implemented, in Outystems, an ontology application applied to the pension solution domain. The objective was to be able to define the pension system of Netherlands from the legislation to the services provided by the company that would result in quotes and contracts being generated by this application. The most interesting and challenging part of this project was to create a new language to represent conditions between properties and concepts of the ontology, so that we could validate the ontology created, and to execute each condition we had to build a parser and an interpreter using javascript with the help of *PeggyJS*, where it could run in a dedicated javascript environment like Azure Function or in the Outsystems server with the integration of a JS engine, *Jint*.

Throughout my time at IG&H, I consistently focused on innovation, problem-solving, and leveraging emerging technologies to deliver impactful solutions. My professional path, from freelancing to senior roles has been shaped by a commitment to continuous learning and adapting to the ever-evolving tech landscape.

Now, I’m eager to dive deeper into cybersecurity, particularly web security and pentesting. This transition feels like a natural extension of my career, allowing me to combine my software engineering expertise with my long-standing interest in cybersecurity.

To kickstart this new chapter, I’ve begun exploring various cybersecurity topics, from setting up home labs to studying for relevant certifications. I’m particularly interested in how web security can be integrated into the development process, ensuring that applications are both functional and secure. As I continue to build my knowledge and skills, I’m excited to see how this journey unfolds and how it will shape my future career.

## Conclusion

As I look back on my career so far, I’m grateful for the experiences and opportunities that have shaped me into the professional I am today. Venturing into cybersecurity is an exciting new chapter, and I’m committed to continuous learning and sharing my journey with the community. I’m looking forward to exploring new frontiers in technology and helping others along the way.

