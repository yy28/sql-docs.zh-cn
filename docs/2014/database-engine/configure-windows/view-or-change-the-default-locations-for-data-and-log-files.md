---
title: 查看或更改数据和日志文件 (SQL Server Management Studio) 的默认位置 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- log files [SQL Server], changing default location
- data files [SQL Server], changing default location
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 46bab09c5115781d85fdb3e7c8fc73e6428322fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018698"
---
# <a name="view-or-change-the-default-locations-for-data-and-log-files-sql-server-management-studio"></a>查看或更改数据文件和日志文件的默认位置 (SQL Server Management Studio)
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中查看和更改新的数据文件和日志文件的默认位置。 默认路径从注册表中获得。 在更改位置后，如果未指定其他位置，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中创建的所有新数据库将使用该位置。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
-   **若要查看或更改的数据和日志文件默认位置，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
-   **跟进：**  [更改默认位置](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Recommendations"></a> 建议  
 保护数据文件和日志文件的最佳做法是确保它们受访问控制列表 (ACL) 保护。 ACL 应设置在创建这些文件的根目录下。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-default-locations-for-database-files"></a>查看或更改数据库文件的默认位置  
  
1.  在对象资源浏览器中，右键单击某个服务器，然后单击“属性”。  
  
2.  在左窗格中，单击 **“数据库设置”** 页。  
  
3.  在 **“数据库默认位置”** 中，查看新的数据文件和日志文件的当前默认位置。 若要更改默认位置，请在 **“数据”** 或 **“日志”** 字段中输入新的默认路径名，或者单击浏览按钮找到并选择路径名。  
  
##  <a name="FollowUp"></a> 跟进： 在更改后的默认位置  
 必须停止并重新启动 SQL Server 服务以完成更改。  
  
## <a name="see-also"></a>请参阅  
 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [创建数据库](../../relational-databases/databases/create-a-database.md)  
  
  
