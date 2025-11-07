

# SimplyShare

A modern Google Drive–style cloud storage app built with **Next.js (React)** and **Spring Boot**. It focuses on smooth uploads, secure file sharing, and instant previews powered by **AWS S3**.

---

## Overview

**SimplyShare** helps users store, organize, and share files in a simple and secure way.

* Upload and manage files and folders
* Share files with other users via email
* Preview images, videos, and PDFs in the browser
* Track storage usage and manage account settings




---

##  Tech Stack

<div align="center">
 <h2> Backend Stack</h2>
</div>  
<div align="center">

| **Layer** | **Technology** | **Purpose** |
| :-------: | :------------- | :----------- |
| **Language** | **Java 21+** <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" width="30" height="30"/> | Core backend language |
| **Framework** | **Spring Boot 3.5.4** <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/spring/spring-original.svg" width="30" height="30"/> | REST APIs, configuration, DI |
| **ORM** | **Spring Data JPA + Hibernate** <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/hibernate/hibernate-original.svg" width="30" height="30"/> | Database mapping & queries |
| **Database** | **MySQL** <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original.svg" width="30" height="30"/> | Store users, folders, and file metadata |
| **Cache** | **Redis** <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/redis/redis-original.svg" width="30" height="30"/> | Cache frequent reads for faster access |
| **Asynchronous** <br>communication  | **Apache Kafka** <img src="https://static.cdnlogo.com/logos/k/35/kafka.svg" width="30" height="30"/> | Asynchronous event-driven processing |
| **Security** | **Spring Security (Session-based)** <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/spring/spring-original.svg" width="30" height="30"/> | Authentication & session management |
| **Email Notification** | **Java Mail Sender** <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" width="30" height="30"/> | Notification & file-sharing emails |
| **Storage** | **AWS S3** <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" width="40" height="30"/>  | File storage using pre-signed URLs |
| **Build Tool** | **Maven** <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/maven/maven-original.svg" width="30" height="30"/> | Build automation & dependency management |
| **Utilities** | **Lombok** <img src="https://avatars.githubusercontent.com/u/45949248?s=200&v=4" width="30" height="30"/> | Reduces Java boilerplate |
| **Documentation** | **Swagger** <img src="https://raw.githubusercontent.com/swagger-api/swagger.io/wordpress/images/assets/SW-logo-clr.png" width="30" height="30"/> | Interactive API documentation |
| **Testing** | **Postman** <img src="https://www.vectorlogo.zone/logos/getpostman/getpostman-icon.svg" width="30" height="30"/> | API testing & workflow automation |

</div>

  <div align="center">
 <h2> Frontend Stack</h2>
  </div>  

<div align="center">

| **Technology** | **Purpose** |
| :------------- | :----------- |
| **Next.js 15+** <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nextjs/nextjs-original.svg" width="30" height="30"/> | React framework for SSR and routing |
| **Tailwind CSS** <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/tailwindcss/tailwindcss-original.svg" width="30" height="30"/> | Utility-first styling |
| **Axios** <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/axios/axios-plain.svg" width="30" height="30"/> | API calls to backend |
</div>

---




## System Architecture
> **Architecture note:** The project currently uses a **monolithic architecture**, implemented in a modular way so it can be split into **microservices** later if needed.

---


```mermaid
graph TD;
  Frontend[Frontend: Next.js + Tailwind]
  Backend[Backend: Spring Boot REST API]
  DB[MySQL: Persistent Data]
  Cache[Redis: Cache Layer]
  Events[Kafka: Event Stream]
  Storage[AWS S3: File Storage]
  Mail[Java Mail Sender: Email Notifications]

  Frontend --> Backend
  Backend --> DB
  Backend --> Cache
  Backend --> Events
  Backend --> Storage
  Backend --> Mail
```

Backend handles authentication, validation, metadata management, caching, and delegates file storage to S3 via pre-signed URLs. Kafka is used for background jobs (logs, notifications), Redis for caching, and MySQL for persistent metadata.


## Key Features

<div align="center">

|          Section | Feature Highlights                                                                                                                                                                                   |
| ---------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|         **Home** | - See last used files and folders  <br> - Quick sidebar/menu for navigation  <br> - “New” button for fast actions  <br> - Toggle list/grid views  <br> - Inline actions: rename, move, share, delete |
|     **My Drive** | - Browse folders and files like a file explorer  <br> - Intuitive tree structure and breadcrumbs                                                                                                     |
|       **Recent** | - Access recently used files instantly  <br> - Switch between list and grid view                                                                                                                     |
|       **Upload** | - Drag-and-drop or browse to select files  <br> - Instant upload with dedicated button  <br> - Preview after upload  <br> - Upload progress tracking                                                 |
|        **Trash** | - View deleted files (recycle bin)  <br> - Restore or permanently delete files                                                                                                                       |
|      **Profile** | - View and update profile  <br> - Check storage usage and stats  <br> - Upload/profile picture  <br> - Update password and enable 2FA                                                                |
|        **Share** | - Share files by entering recipient email  <br> - Generate secure links and revoke access                                                                                                            |
| **Subscription** | - See current plan details  <br> - Upgrade/downgrade plans  <br> - View invoices and billing info                                                                                                    |
|    **Previewer** | - Preview images and play videos inline  <br> - View & edit PDFs with annotations, text, drawing  <br> - Download edited/previewed files without extra software                                      |

</div>

---

## Security

<div align="center">

|         Aspect | Details                                                                        |
| -------------: | :----------------------------------------------------------------------------- |
| Authentication | Session-based auth using Spring Security; secure cookie + server session store |
|      Passwords | Stored hashed with BCrypt; server-side validation on change/reset              |
|  Authorization | Role-based checks on endpoints and UI (admin vs user)                          |
|   Input Safety | Request validation, size limits,                      |
| Session Safety | HttpOnly secure cookies, same-site policy, session expiry and invalidation     |

</div>

---

## Performance & Scalability

<div align="center">

|       Optimization | Benefit                                                    |
| -----------------: | :--------------------------------------------------------- |
|      Redis caching | Lowers DB load, speeds repeated reads                      |
| Kafka event stream | Offloads heavy jobs (emails, logs) from request path       |
| S3 pre-signed URLs | Frontend uploads directly to S3 — reduces server bandwidth |
| HikariCP (DB pool) | Efficient DB connections and stable throughput             |

</div>

---

## Project Info

 <h2 align="center">
 
   SimplyShare</b> — A cloud storage platform inspired by Google-Drive
   
</h2>
   
<div align="center">

<table>
  <tr>
    <th> Duration</th>
    <td><b>4 weeks</b> (Full Backend + Frontend Development)</td>
  </tr>
  <tr>
    <th> Tech Stack</th>
    <td><b>Spring Boot · MySQL · Redis · Kafka · AWS S3 · Next.js</b></td>
  </tr>
  <tr>
    <th> Live Demo</th>
    <td><a href="https://simplyshare.projectswithsurja.dev" target="_blank">simplyshare.projectswithsurja.dev</a></td>
  </tr>
  <tr>
    <th> Deployment</th>
    <td><b>AWS EC2</b> for backend · <b>Vercel</b> for frontend</td>
  </tr>
</table>

</div>


---
## Developer's contact
---
<div align="center">
  
  <!-- Profile Image -->
  <img src="https://avatars.githubusercontent.com/u/00000000?v=4" width="130" style="border-radius: 50%; border: 3px solid #ccc;" alt="Developer Profile Picture"/>

  <!-- Name & Role -->
  <h2><b>Surja Kumar Jana</b></h2>
  <p><i>Aspiring Backend Developer | (Java • Spring Boot • MySQL • AWS)</i></p>
  <p>📍 India</p>

  <!-- Contact Badges -->
  <p>
    <a href="mailto:janaofficial0110@gmail.com">
      <img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/>
    </a>
    <a href="https://github.com/SurjaKumarJana"  target="_blank">
      <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"/>
    </a>
    <a href="https://www.linkedin.com/in/surjakumarjana" target="_blank">
      <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/>
    </a>
  </p>

  <!-- Motto -->
  <p align="center">
    💬 <i>“Building scalable backend systems with Java and gradually expanding into Full Stack Development.”</i>
  </p>

</td>


</div>

---

This is a personal practice project to learn and apply modern full-stack and backend technologies. The design is intentionally modular so the monolith can be split into microservices later.

---

*Thank you — SimplyShare*
