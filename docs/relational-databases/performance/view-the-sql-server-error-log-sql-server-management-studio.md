---
title: "查看 SQL Server 错误日志 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "07/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "查看日志"
  - "显示日志"
  - "错误 [SQL Server], 日志"
  - "日志 [SQL Server], SQL Server 错误日志"
  - "日志 [SQL Server], 查看"
ms.assetid: 55f468ba-146c-4ab3-95cd-d35d051afd12
caps.latest.revision: 14
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 14
---
# 查看 SQL Server 错误日志 (SQL Server Management Studio)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志包含进行故障排除所需的用户定义事件和某些系统事件。 
  

  ## 如何查看日志
1.  在 SSMS 中，选择“对象资源管理器”

>**打开**对象资源管理器的步骤：键盘快捷方式为 **F8**。 或者，在顶部菜单中单击“视图”/“对象资源管理器”![Object_explorer](../../relational-databases/performance/media/object-explorer.png) 


2.  在“对象资源管理器”中，连接到某个 SQL Server 实例，然后展开该实例。
  
3.  找到并展开“管理”部分（假设你有权查看它）。

4.  右键单击“SQL Server 日志”，选择“查看”，然后选择“查看 SQL Server 日志”。
 ![View_SQLServer_Log_SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5.  将显示日志文件查看器（可能需要一分钟），其中包含一个日志列表供你查看。
  
6. 一些人推荐 [MSSQLTips.com](https://www.mssqltips.com/) 上的实用帖 [Identify location of the SQL Server Error Log file](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/)（确定 SQL Server 错误日志文件的位置）。 帖子中提供了许多很棒的信息，请务必了解这些信息！
  
  