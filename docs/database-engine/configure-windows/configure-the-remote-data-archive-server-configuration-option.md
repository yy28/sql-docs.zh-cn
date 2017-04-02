---
title: "配置远程数据存档服务器配置选项 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b5817b5a-f39a-4faf-b11e-a47b54fd9f32
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# 配置远程数据存档服务器配置选项
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 **remote data archive** 选项，可以指定能否为服务器上的数据库和表启用延伸。 有关详细信息，请参阅 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)。  
  
 **remote data archive** 选项可以具有下列值。  
  
|值|说明|  
|-----------|-----------------|  
|0|不可以为服务器上的数据库和表启用延伸。|  
|1|可以为服务器上的数据库和表启用延伸。|  
  
 必须具有 sysadmin 或 serveradmin 权限，才能运行 **sp_configure** 来设置**远程数据存档**选项的值。  
  
## 示例  
 下面的示例先显示 **remote data archive** 选项的当前设置。 然后，此示例通过将 **remote data archive** 选项的值设置为 1 来启用这个选项。  
  
```  
EXEC sp_configure 'remote data archive';  
GO  
EXEC sp_configure 'remote data archive' , '1';  
GO  
RECONFIGURE;  
GO  
```  
  
 若要禁用该选项，请将此值设置为 0。  
  
## 另请参阅  
 [为数据库启用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  