---
title: Remote Debugger
date: 2023-04-23
description: Microsoft Orleans.
link-title: Orleans
draft: false
authorbox: false
comments: true
thumbnail:
    src: "img/vsremotedebugger.jpg"
visibility:
- list
menu:
    main:
        name: Remote Debugger
        weight: 10
tags:
- visualstudio
- remotedebugger
series:
 - visualstudio
---
دیباگ پروژه های .NET بر روی IIS با استفاده از Visual Studio
<!--more-->

در این مطلب قصد داریم باهم قابلیت خفن Visual Studio رو که میشه وصل شد به IIS و پروژه رو دیباگ کرد صحبت کنیم
در مرحله اول باید Remote Debugger رو نسبت به نسخه Visual Studio که استفاده میکنید از سایت [مایکروسافت](https://learn.microsoft.com/en-us/visualstudio/debugger/remote-debugging?view=vs-2022) دانلود کنید.
<!--more-->
![Visual Studio Remote Debugger](/img/visualstudioremotedebuggermicrosoftpage.jpg)
<!--more-->

بعد از نصب کردن Remote Debugger 
باید اجازه دسترسی به Netwrok رو به Remote Debugger بدیم که پورت 4026 رو داخل فایروال اضافه کنه

<!--more-->

![remoteDebuggerFireWall.PNG](/img/remoteDebuggerFireWall.PNG)
<!--more-->

و حتما دقت کنید که Remote Debugger رو بصورت Run As Administrator اجرا کنید

![remoteDebugger.PNG](/img/remoteDebugger.PNG)
<!--more-->

در تب Tools -> Options
میتونیم پورتی که با Visual Studio میخوایم بهش وصل بشیم رو مشخص کنیم که بصورت پیشفرض 4026 است
در قسمت  Authentication Mode یوزری که میخوایم با اون به سرور وصل بشیم رو مشخص میکنیم
اگر میخواین بصورت Anonymous به سرور متصل بشین گزینه No Authentication انتخاب کنید
<!--more-->

![remoteDebuggerOptionTab.PNG](/img/remoteDebuggerOptionTab.PNG)

<!--more-->
Mode پابلیش رو هم حتما روی Debug قرار بدین
![visualStudioPublishDebug.png](/img/visualStudioPublishDebug.png)

<!--more-->
بعد از اینکه DLL های پابلیش شده رو داخل سرور کپی کردیم
از Visual Studio منوی Debug گزینه Attach To Process رو انتخاب میکنیم
<!--more-->
![visualStudioDebugTab.png](/img/visualStudioDebugTab.png)

<!--more-->
پنجره زیر باز میشود
<!--more-->
![debuggerWindow.PNG](/img/debuggerWindow.PNG)
<!--more-->
در باکس Connection Type IP سرور مورد نظر رو بزنین
و در داخل Filter Process
w3w رو سرچ کنید تا Process های IIS رو فیلتر کنه
<!--more-->
![debuggerAttachToProcess.PNG](/img/debuggerAttachToProcess.PNG)
<!--more-->
در نهایت هر درخواستی که به Api هاست شده روی IIS بیاد میتونید دیباگ کنید
<!--more-->
![debugVisualStudio.PNG](/img/debugVisualStudio.PNG)