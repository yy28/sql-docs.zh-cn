---
title: 将 Sybase ASE 架构映射到 SQL Server 架构 (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2e06a6710b85621f9b0df66f38c42a0b8ebc05ce
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>将 Sybase ASE 架构映射到 SQL Server 架构 (SybaseToSQL)
在 Sybase 自适应 Server Enterprise (ASE)，每个数据库都有一个或多个架构。 默认情况下，SSMA 将中的数据库和架构的所有对象都迁移到同一个数据库和架构中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 但是，你可以自定义 ASE 之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库和架构。  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE 和 SQL Server 或 SQL Azure 架构  
ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库以及它们的架构使用两个部分表示法指定作为*database.schema*。 例如，在 ASE**演示**数据库，可能有**dbo**架构。 数据库和架构对被指定为**demo.dbo**。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 具有相同的数据库和架构，对也被指定为**demo.dbo**。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目标数据库和架构  
在 SSMA，可以将一个 ASE 架构映射到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 架构。  
  
**若要修改的数据库和架构**  
  
1.  在 Sybase 元数据资源管理器中，选择**数据库**。  
  
    **架构映射**时选择单独的数据库，，可能也是可用选项卡**架构**文件夹或单个架构。 中的列表**架构映射**选项卡上自定义的所选对象。  
  
2.  在右窗格中，单击**架构映射**选项卡。  
  
    你将看到具有目标值后跟其架构的所有 ASE 数据库的列表。 此目标中，表示在由两部分表示法 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或对象和数据将迁移的 SQL Azure。  
  
3.  选择包含你想要更改，然后单击的映射的行**修改**。  
  
4.  在**选择目标架构**对话框中，你可以浏览可用的目标数据库和架构或类型的数据库和架构中由两部分表示法 (database.schema) 的文本框的名称，然后单击**确定**。  
  
5.  目标上的更改**架构映射**选项卡。  
  
**映射模式**  
  
-   将映射到 SQL Server  
  
可以将源数据库映射到任何目标数据库。 默认情况下映射源数据库到目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]具有与其连接使用 SSMA 数据库。 要映射的目标数据库是否不存在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，则系统将提示你使用的消息**"目标中不存在的数据库和/或架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据。它会在同步期间创建。是否要继续？"** 单击是。 同样，可以架构映射到在目标下不存在架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库将在同步期间创建的。  
  
-   将映射到 SQL Azure  
  
到连接的目标 SQL Azure 数据库或连接的目标 SQL Azure 数据库中的任何架构，你可以映射源数据库。 如果将源架构映射到已连接的目标数据库在任何非现有架构，则系统将提示您提供一条消息**"架构中不存在目标元数据。它会在同步期间创建。你想要继续吗？"**单击是。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>还原为默认数据库和架构  
如果你自定义 ASE 架构之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 架构，你可以还原回默认值的映射。  
  
**若要还原到的默认数据库和架构**  
  
1.  在架构映射的选项卡上，选择任何行，然后单击**重置为默认**若要还原到的默认数据库和架构。  
  
## <a name="next-steps"></a>后续步骤  
如果你想要分析的 Sybase ASE 对象转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象，你可以[创建转换报表](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c)。 否则，你可以[转换 ASE 数据库对象定义](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3)到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象定义。  
  
## <a name="see-also"></a>另请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server 的 Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
