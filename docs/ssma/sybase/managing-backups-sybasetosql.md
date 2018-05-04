---
title: 管理备份 (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Managing Backups
ms.assetid: 266d987c-ecc5-4fa4-bfdf-8c584f1a1332
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ccd05bac91bb0e394a046852659a42ce549d52bf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="managing-backups-sybasetosql"></a>管理备份 (SybaseToSQL)
Sybase 备份管理允许你备份和还原表数据之前或之后运行测试。 你还可以管理与管理备份内容对话框备份内容。  
  
## <a name="sybase-backup-management"></a>Sybase 备份管理  
  
### <a name="backup"></a>Backup  
若要打开备份对话框，在测试人员菜单上，指向 Sybase 备份管理，然后单击备份... 在备份对话框中，你会发现显示加载的 Sybase 架构的所有表的 Sybase 元数据树。 选择要执行备份的一个或多个表。  
  
以下按钮位于对话框：  
  
-   单击**检查状态**按钮来检查表的备份状态。  
  
-   单击**备份**按钮以备份表的数据。  
  
-   单击**取消**按钮以关闭对话框。  
  
### <a name="restore"></a>还原  
若要打开还原对话框中，在测试人员菜单中指向 Sybase 备份管理，然后单击还原... 那里您会发现树包含在备份中可用的表。 选择一个或多个要还原其数据的表。  
  
以下按钮位于对话框：  
  
-   单击**检查状态**按钮来检查表的备份状态。  
  
-   单击**还原**按钮以还原到表的备份数据。  
  
-   单击**取消**按钮以关闭对话框。  
  
### <a name="managing-backup-contents"></a>管理备份内容  
若要打开管理备份内容，在测试人员菜单上，指向 Sybase 备份管理然后单击备份内容... 那里您会发现树包含在备份中的表。  
  
以下按钮位于对话框：  
  
-   单击**检查状态**按钮来检查表的备份状态。  
  
-   单击**删除**按钮可从备份中删除该表。  
  
-   单击**关闭**按钮以关闭对话框。  
  
## <a name="sql-server-backup-management"></a>SQL Server 备份管理  
SQL Server 备份管理允许你备份和还原表数据之前或之后运行测试。 你还可以管理与管理备份内容对话框备份内容。  
  
### <a name="backup"></a>Backup  
若要打开备份对话框，在测试人员菜单上，指向 SQL Server 备份管理，然后单击备份... 在备份对话框中，你会发现显示加载的 SQL Server 数据库的所有表的 SQL 服务器元数据树。 选择要执行备份的一个或多个表。  
  
以下按钮位于对话框：  
  
-   单击**检查状态**按钮来检查表的备份状态。  
  
-   单击**备份**按钮备份表的数据。  
  
-   单击**取消**按钮以关闭对话框。  
  
### <a name="restore"></a>还原  
若要打开还原对话框中，在测试人员菜单上指向 SQL Server 备份管理中，单击还原... 那里您会发现树包含在备份中可用的表。 选择一个或多个要还原其数据的表。  
  
以下按钮位于对话框：  
  
-   单击**检查状态**按钮来检查表的备份状态。  
  
-   单击**还原**按钮以还原到表的备份数据。  
  
-   单击**取消**按钮以关闭对话框。  
  
### <a name="managing-backup-contents"></a>管理备份内容  
若要打开管理备份内容，在测试人员菜单上，指向 SQL Server 备份管理中，然后单击备份内容... 那里您会发现树包含在备份中的表。  
  
以下按钮位于对话框：  
  
-   单击**检查状态**按钮来检查表的备份状态。  
  
-   单击**删除**按钮可从备份中删除该表。  
  
-   单击**关闭**按钮以关闭对话框。  
  
## <a name="see-also"></a>另请参阅  
[测试迁移的数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
