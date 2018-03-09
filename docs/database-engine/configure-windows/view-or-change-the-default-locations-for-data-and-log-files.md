---
title: "查看或更改数据文件和日志文件的默认位置 | Microsoft Docs"
ms.custom: 
ms.date: 06/13/2017
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
- log files [SQL Server], changing default location
- data files [SQL Server], changing default location
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2f5d4d317ce451cd9080142589817118653a7019
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="view-or-change-the-default-locations-for-data-and-log-files"></a>查看或更改数据文件和日志文件的默认位置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
 保护数据文件和日志文件的最佳做法是确保它们受访问控制列表 (ACL) 保护。 对创建这些文件的根目录设置 ACL。  
 
  
## <a name="view-or-change-the-default-locations-for-database-files"></a>查看或更改数据库文件的默认位置  
  
1.  在对象资源浏览器中，右键单击你的服务器，然后单击“属性”。  
  
2.  在该“属性”页的左面板中，单击“数据库设置”选项卡。  
  
3.  在 **“数据库默认位置”**中，查看新的数据文件和日志文件的当前默认位置。 若要更改默认位置，请在 **“数据”** 或 **“日志”** 字段中输入新的默认路径名，或者单击浏览按钮找到并选择路径名。  
  
>**注意：** 更改默认位置之后，必须停止并重新启动 SQL Server 服务以完成更改。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [创建数据库](../../relational-databases/databases/create-a-database.md)  
  
  
