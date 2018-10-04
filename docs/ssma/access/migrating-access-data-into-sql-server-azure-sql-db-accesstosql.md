---
title: 访问数据迁移到 SQL Server-Azure SQL DB (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- bulk loading data
- data, loading into SQL Azure
- data, loading into SQL Server
- migrating databases, loading data
- migrating databases, options
- options, migrating data
- SQL Azure, migrating data into
- SQL Server, migrating data into
ms.assetid: f3b18af7-1af0-499d-a00d-a0af94895625
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ab3ce18b1b79951c76b34be3f90b2d8782ba64e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773816"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>访问数据迁移到 SQL Server-Azure SQL DB (AccessToSQL)
已成功创建数据库对象后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以将数据迁移从 Access 到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
## <a name="setting-migration-options"></a>设置迁移选项  
在迁移到的数据之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，查看中的项目迁移选项**项目设置**对话框。 在此对话框中，可以设置迁移批大小、 表锁定、 约束检查，插入触发器激发，标识和 null 值处理，以及如何处理带日期[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]范围。 有关详细信息，请参阅[项目设置 （迁移）](http://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)。  
  
## <a name="migrating-data"></a>将数据迁移  
迁移数据是大容量加载操作，将数据加载到行移动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中的事务。 要加载到的行数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或项目设置中配置 SQL Azure 中的每个事务。  
  
若要查看迁移的消息，请确保输出窗格中可见。 如果不是，在**视图**菜单中，选择**输出**。  
  
**若要将数据迁移**  
  
1.  请确保你已加载到了访问数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
2.  在访问元数据资源管理器，选择包含你想要迁移的数据的对象：  
  
    -   若要迁移整个数据库的数据，请选择数据库名称旁边的复选框。  
  
    -   若要将数据迁移单个表中，展开数据库，展开**表**，然后选择表旁边的复选框。 若要省略单个表中的数据，清除复选框。  
  
3.  右键单击**数据库**，然后选择**迁移数据**。  
  
此外可以迁移使用的数据之外 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bcp**命令行实用程序或[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 有关这些工具的详细信息，请参阅[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
## <a name="next-step"></a>下一步  
如果您已访问的数据库应用程序想要继续使用迁移后，链接到访问数据库表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表。 有关详细信息，请参阅[链接访问应用程序到 SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)。  
  
## <a name="see-also"></a>请参阅  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[设置转换和迁移选项](setting-conversion-and-migration-options-accesstosql.md)  
  
