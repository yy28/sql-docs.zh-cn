---
title: "移动数据库文件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "灾难恢复 [SQL Server], 移动数据库文件"
  - "文件 [SQL Server], 移动"
  - "数据文件 [SQL Server], 移动"
  - "文件移动 [SQL Server]"
  - "移动全文目录"
  - "移动数据库"
  - "全文目录 [SQL Server], 移动"
  - "移动数据库文件"
  - "计划的磁盘维护 [SQL Server]"
  - "移动文件"
  - "重定位数据库文件"
  - "计划的数据库重定位 [SQL Server]"
  - "数据库 [SQL Server], 移动"
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 移动数据库文件
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，可以通过在 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 语句的 FILENAME 子句中指定新的文件位置来移动系统数据库和用户数据库。 数据、日志和全文目录文件也可以通过此方法进行移动。 这在下列情况下可能很有用：  
  
-   故障恢复。 例如，由于硬件故障，数据库处于可疑模式或被关闭。  
  
-   预先安排的重定位。  
  
-   为预定的磁盘维护操作而进行的重定位。  
  
## 本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[移动用户数据库](../../relational-databases/databases/move-user-databases.md)|说明将用户数据库文件和全文目录文件移动到新位置的过程。|  
|[移动系统数据库](../../relational-databases/databases/move-system-databases.md)|说明将系统数据库文件移动到新位置的过程。|  
  
## 另请参阅  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  