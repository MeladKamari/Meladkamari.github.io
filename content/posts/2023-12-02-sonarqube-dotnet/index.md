---
title: Sonarqube
date: 2023-04-23
description: Sonarqube .Net Example .
link-title: Sonarqube
draft: true
authorbox: false
comments: true
thumbnail:
    src: "img/sonarqube.jpg"
visibility:
- list
menu:
    main:
        name: Sonarqube
        weight: 10
tags:
- Sonarqube
- .Net
series:
 - Sonarqube
---
SonarQube: ابزار اساسی برای توسعه‌دهندگان به سوی کدی تمیز و ایمن
<!--more-->
SonarQube یک ابزار متن‌باز برای ارزیابی کیفیت کد و تحلیل آن است. این ابزار به توسعه‌دهندگان و تیم‌های توسعه کمک می‌کند تا بهبود کیفیت کد، کاهش بدهی فنی (technical debt)، و جلوگیری از ایجاد مشکلات امنیتی را انجام دهند.
<!--more-->
*	از قابلیت های SonarQube میتوان به ارزیابی Code Base  برای تحلیل کیفیت کد
*	تحلیل اصول برنامه نویسی SOLID  ، تجزیه و تحلیل تعداد باگ ها ، زمان اجرا ، Code Coverage
*	این ابزار قابلیت تحلیل امنیتی را نیز دارد و به برنامه نویس ان کمک میکند تا مشکلات امنیتی را در کد خود شناسایی و رفع کنند.
*	گزارشات جامعی از کیفیت کد ، تغییرات جدید را ارائه میدهد که به  برنامه نویسان و مدیران پروژه کمک میکند تا روند تولید پروژه را مدیریت کنند.
*   قابلیت ادغام شدن با فرآیند توسعه مداومCI/CD
<!--more-->
SonarQube  برای ذخیره سازی اطلاعات تحلیلی از دیتابیس های H2 , PostgreSQL , MySQL , Microsoft SQL Server , Oracle پشتیبانی میکند و  **خود دارای دیتابیس  Internal است اما برای محیط های Production توصیه نمی شود**.
<!--more-->

SonarQube دارای Edition مختلفی است و در این مقاله از  Community Edition   استفاده میکنیم که از زبان های گوناگونی پشتیبانی میکند نظیر
**Java
JavaScript
C#
C/C++
Python
Ruby
TypeScript
HTML
CSS
PHP
Swift
Objective-C
PL/SQL
Go
Kotlin
Scala** 
<!--more-->
برای اجرا کردن SonarQube فایل [docker-compose.yml](https://raw.githubusercontent.com/MeladKamari/Sonarqube-Sample-Project/master/docker-compose.yml)  را اجرا کنید.
<!--more-->

```yaml
version: '2'
services:
  postgresql:
    image: 'bitnami/postgresql:latest'
    ports:
      - '5444:5432'
    volumes:
      - 'postgresql_data:/bitnami'
    environment:
      - ALLOW_EMPTY_PASSWORD=yes
  sonarqube:
    image: 'sonarqube:community'
    ports:
      - '9000:9000'
    environment:
      - POSTGRESQL_HOST=postgresql
      - POSTGRESQL_PORT=5444
      - POSTGRESQL_ROOT_USER=postgres
      - POSTGRESQL_CLIENT_CREATE_DATABASE_NAME=bitnami_sonarqube
      - POSTGRESQL_CLIENT_CREATE_DATABASE_USERNAME=bn_sonarqube
      - POSTGRESQL_CLIENT_CREATE_DATABASE_PASSWORD=bitnami1234
      - SONARQUBE_DATABASE_NAME=bitnami_sonarqube
      - SONARQUBE_DATABASE_USER=bn_sonarqube
      - SONARQUBE_DATABASE_PASSWORD=bitnami1234
    volumes:
      - sonarqube_data:/bitnami
volumes:
  sonarqube_data:
    driver: local
  postgresql_data:
    driver: local
```


<!--more-->
یا با این  Command میتوانید SonarQube را اجرا کنید
<!--more-->
```bash
 curl -O https://raw.githubusercontent.com/MeladKamari/Sonarqube-Sample-Project/master/docker-compose.yml docker-compose up
```
<!--more-->
