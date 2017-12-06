---
title: "将访问数据迁移到 SQL Server 的 Azure SQL DB (AccessToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: "17"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8b9e885b397abc05af7ec538eb2ed46c8ba12ea2
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>将访问数据迁移到 SQL Server 的 Azure SQL DB (AccessToSQL)
您已成功创建数据库对象插入后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你可以访问到从迁移数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
## <a name="setting-migration-options"></a>设置迁移选项  
在迁移到的数据之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，查看中的项目迁移选项**项目设置**对话框。 在此对话框中，你可以设置迁移批处理大小、 表锁定、 约束检查，插入触发器触发，标识和 null 值处理，以及如何处理外出时的日期[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]范围。 有关详细信息，请参阅[项目设置 （迁移）](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d)。  
  
## <a name="migrating-data"></a>将数据迁移  
迁移数据是一大容量加载操作，将数据插入的行移[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或在事务中的 SQL Azure。 要被加载进的行数[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或在项目设置中配置在各事务中的 SQL Azure。  
  
若要查看迁移消息，请确保输出窗格中可见。 如果不是，在**视图**菜单上，选择**输出**。  
  
**若要将数据迁移**  
  
1.  请确保你已加载到访问数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
2.  在访问元数据资源管理器，选择包含你想要迁移的数据的对象：  
  
    -   若要将为整个数据库的数据迁移，选择数据库名称旁边的复选框。  
  
    -   若要将数据迁移从各个表中，展开数据库，展开**表**，然后选择表旁边的复选框。 若要省略各个表中的数据，请清除复选框。  
  
3.  右键单击**数据库**，然后选择**迁移数据**。  
  
您也可以将迁移 SSMA 之外的数据使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **bcp**命令行实用工具或[!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]。 有关这些工具的详细信息，请参阅[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="next-step"></a>下一步  
如果你拥有访问你想要继续迁移后使用的数据库应用程序，链接到 Access 数据库表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 表。 有关详细信息，请参阅[链接访问应用程序到 SQL Server](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4)。  
  
## <a name="see-also"></a>另请参阅  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[设置转换和迁移选项](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167)  
  
