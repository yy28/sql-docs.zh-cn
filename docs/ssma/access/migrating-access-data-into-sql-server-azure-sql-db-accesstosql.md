---
title: 将 Access 数据迁移到 SQL Server-Azure SQL DB （AccessToSQL） |Microsoft Docs
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
ms.openlocfilehash: 8f0e93efee0c57c904c32ec52fbb560f973f21b8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67907147"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>将 Access 数据迁移到 SQL Server-Azure SQL DB （AccessToSQL）
成功将数据库对象创建到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]后，可以将数据从访问迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
## <a name="setting-migration-options"></a>设置迁移选项  
在将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 之前，请在 "**项目设置**" 对话框中查看项目迁移选项。 在此对话框中，您可以设置迁移批大小、表锁定、约束检查、插入触发器触发、标识和 null 值处理，以及如何处理超出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]范围的日期。 有关详细信息，请参阅[项目设置（迁移）](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)。  
  
## <a name="migrating-data"></a>迁移数据  
迁移数据是一项大容量加载操作，用于将数据行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移入或移入事务中 SQL Azure。 在项目设置中配置每个事务[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中要加载到或 SQL Azure 的行数。  
  
若要查看迁移消息，请确保输出窗格可见。 如果不是，则在 "**视图**" 菜单上选择 "**输出**"。  
  
**迁移数据**  
  
1.  请确保已将 Access 数据库对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
2.  在 "Access 元数据资源管理器" 中，选择包含要迁移的数据的对象：  
  
    -   若要迁移整个数据库的数据，请选中数据库名称旁边的复选框。  
  
    -   若要从单个表中迁移数据，请展开数据库，展开 "**表**"，然后选中表旁边的复选框。 若要忽略各个表中的数据，请清除该复选框。  
  
3.  右键单击 "**数据库**"，然后选择 "**迁移数据**"。  
  
你还可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bcp**命令行实用程序或[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]在 SSMA 外部迁移数据。 有关这些工具的详细信息，请[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]参阅联机丛书。  
  
## <a name="next-step"></a>下一步  
如果您的 Access 数据库应用程序要在迁移后继续使用，请将 Access 数据库表链接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 表。 有关详细信息，请参阅[将访问应用程序链接到 SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)。  
  
## <a name="see-also"></a>另请参阅  
[将 Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[设置转换和迁移选项](setting-conversion-and-migration-options-accesstosql.md)  
  
