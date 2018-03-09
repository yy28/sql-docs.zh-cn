---
title: "Database Mail XPs 服务器配置选项 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Database Mail XPs option
- Database Mail [SQL Server], enabling
ms.assetid: e22c4e63-1792-473b-af11-14a7931ca9ed
caps.latest.revision: "20"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 32fdd1b3a13e0275e7c1a8fce596a382a59d32ae
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="database-mail-xps-server-configuration-option"></a>Database Mail XPs 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 **DatabaseMail XPs** 选项可以在此服务器上启用数据库邮件。 可能的值有：  
  
-   **0** 表示数据库邮件不可用（默认值）。  
  
-   **1** 表示数据库邮件可用。  
  
 该设置立即生效，无需停止并重新启动服务器。  
  
 启用数据库邮件后，必须配置一个数据库邮件主机数据库，才能使用 Database Mail。  
  
 使用 **数据库邮件配置向导** 配置数据库邮件可以启用 **msdb** 数据库中的数据库邮件扩展存储过程。 如果你使用的是 **数据库邮件配置向导**，则不需要使用下面的 **sp_configure** 示例。  
  
 将 **Database Mail XPs** 选项设置为 0 可以防止启动数据库邮件。 如果该选项设置为 0 时数据库邮件正在运行，则其将继续运行并发送邮件，直到数据库邮件空闲时间达到 **DatabaseMailExeMinimumLifeTime** 选项中配置的时间。  
  
## <a name="examples"></a>示例  
 以下示例启用了 Database Mail 扩展存储过程。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Database Mail XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)  
  
  
