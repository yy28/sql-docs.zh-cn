---
title: "SQL Server 2016 的 SQL Server Reporting Services 中的重大更改 | Microsoft Docs"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Me.Value 引用"
  - "Reporting Services, 向后兼容性"
  - "重大更改 [Reporting Services]"
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
caps.latest.revision: 121
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 116
---
# SQL Server 2016 的 SQL Server Reporting Services 中的重大更改
  本主题介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中的重大更改。 这些更改可能导致基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的早期版本的应用程序、脚本或功能无法继续使用。 您在升级时，或在自定义脚本或报表中可能会遇到这些问题。  
  
  ## 安全扩展插件
  
  自定义安全扩展插件需要进行某些修改，才可使用新 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]。 安全扩展插件需要使用 IAuthenticationExtension2 接口。
  
  ## WMI 提供程序
  
  [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 应用程序名称从 "ReportManager" 更改为 "ReportServerWebApp"。
  
## 另请参阅  
 [SQL Server 2016 中 SQL Server Reporting Services 的行为更改](http://msdn.microsoft.com/zh-cn/2a767f0f-84f2-4099-8784-1e37790f858e)   
 [Reporting Services (SSRS) 中的新功能](../Topic/What's%20New%20in%20Reporting%20Services%20\(SSRS\).md)   
 [SQL Server 2016 的 SQL Server Reporting Services 中不推荐使用的功能](http://msdn.microsoft.com/zh-cn/3876c01e-f81d-4cce-9104-5106a8c369e6)   
 [SQL Server 2016 的 SQL Server Reporting Services 中停止使用的功能](http://msdn.microsoft.com/zh-cn/d529cc96-3483-480b-9bfc-bd28b1d0ef52)  
  
  