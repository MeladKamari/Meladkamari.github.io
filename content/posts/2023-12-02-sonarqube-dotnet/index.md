---
title: Sonarqube
date: 2023-12-02
description: Sonarqube .Net Example .
link-title: Sonarqube
draft: false
authorbox: false
comments: true
thumbnail:
    src: "img/sonarqube-dotnet/sonarqube.jpg"
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
*	این ابزار قابلیت تحلیل امنیتی را نیز دارد و به برنامه نویسان کمک میکند تا مشکلات امنیتی را در کد خود شناسایی و رفع کنند.
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
برای اجرا کردن SonarQube فایل [docker-compose.yml](https://raw.githubusercontent.com/MeladKamari/Sonarqube-Sample-Project/master/docker-compose.yml)  را اجرا کنید
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
یا با این  Command میتوانید SonarQube را اجرا کنید .
<!--more-->
```bash
 curl -O https://raw.githubusercontent.com/MeladKamari/Sonarqube-Sample-Project/master/docker-compose.yml docker-compose up
```
<!--more-->
SonarQube در پورت 9000 در دسترس است  و با  admin admin میتوان لاگین کرد.
<!--more-->
![sonarqube-login-page.jpg](/img/sonarqube-dotnet/sonarqube-login-page.jpg)
<!--more-->
SonarQube قابلیت اتصال به Source Control های **AzureDevOps, Github, BitbucketCloud, Gitlab, BitBucketServer**
را دارد.
<!--more-->
**SonarQube برای اجرا نیاز به [JDK JAVA](https://www.oracle.com/java/technologies/downloads/) دارد و حتما آن را روی نسخه کلاینت نصب کنید.**
<!--more-->
برای دسترسی به Command های SonarQube کد زیر را در ترمینال اجرا کنید.
```bash
dotnet tool install --global dotnet-sonarscanner
```
در SonarQube روی Create a local project کلیک میکنیم تا پروژه جدیدی ساخته شود.

![sonarqube-create-a-local-project.jpg](/img/sonarqube-dotnet/sonarqube-create-a-local-project.jpg)

در این صفحه اطلاعات پروژه را وارد میکنیم و **Project Key** منحصر به فردی را به پروژه اختصاص میدهیم. 

![sonarqube-create-a-local-project-input.jpg](/img/sonarqube-dotnet/sonarqube-create-a-local-project-input.jpg)
<!--more-->
مرحله بعدی baseline مورد نیاز برای پروژه را انتخاب میکنیم .
![set-up-project-for-clean-as-you-code.jpg](/img/sonarqube-dotnet/set-up-project-for-clean-as-you-code.jpg)
پروژه در SonarQube ساخته شد مرحله بعدی ساخت Access Token برای دسترسی به SonarQube است .
<!--more-->
درمنوی My Account 
<!--more-->
![account.jpg](/img/sonarqube-dotnet/account.jpg)
<!--more-->
تب  Token  , Security  جدیدی ایجاد میکنیم.
<!--more-->
![generate-token.jpg](/img/sonarqube-dotnet/generate-token.jpg)

 حال با استفاده از Command , **Token - URL - Project Key** های زیر را اجرا میکنیم تا Metric ها به سرور SonarQube ارسال شود.

```bash
dotnet sonarscanner begin /k:"CNL" /d:sonar.host.url=http://192.168.126.131:9000 /d:sonar.token=sqp_f70e2686968ebd3ba0af83678e8f5433cbb1a654
dotnet build 
dotnet sonarscanner end /d:sonar.token=sqp_f70e2686968ebd3ba0af83678e8f5433cbb1a654
```
<!--more-->
بعد از ارسال Metric ها به سرور SonarQube در Dashboard  میتوان وضعیت  Code base را مشاهده کرد.  
<!--more-->
![quality-gate-status.jpg.jpg](/img/sonarqube-dotnet/quality-gate-status.jpg)


[لینک گیت هاب پروژه](https://github.com/MeladKamari/Sonarqube-Sample-Project)
