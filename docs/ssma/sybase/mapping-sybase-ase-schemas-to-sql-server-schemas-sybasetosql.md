---
title: Sybase ASE 架构映射到 SQL Server 架构 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
ms.openlocfilehash: b2250ded7d76ad35de8ad960356d272358201e37
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38985099"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Sybase ASE 架构映射到 SQL Server 架构 (SybaseToSQL)
在 Sybase Adaptive Server Enterprise (ASE)，每个数据库都有一个或多个架构。 默认情况下，SSMA 将数据库和架构中的所有对象都迁移到同一个数据库和架构中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 但是，自定义 ASE 之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库和架构。  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE 和 SQL Server 或 SQL Azure 架构  
ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库和其架构使用两个部分表示法指定作为*database.schema*。 例如，在 ASE**演示**数据库，可能会有**dbo**架构。 数据库和架构对被指定为**demo.dbo**。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 有相同的数据库和架构，将对也被指定为**demo.dbo**。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目标数据库和架构  
在 SSMA 中，可以将 ASE 架构映射到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 架构。  
  
**若要修改的数据库和架构**  
  
1.  在 Sybase 元数据资源管理器中，选择**数据库**。  
  
    **架构映射**选项卡，也可选择单独的数据库，当**架构**文件夹或单个架构。 中的列表**架构映射**所选对象的自定义选项卡。  
  
2.  在右窗格中，单击**架构映射**选项卡。  
  
    您将看到所有 ASE 使用的数据库及其架构和目标值列表。 此目标中的两个部分表示法表示 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象和数据都迁移。  
  
3.  选择包含你想要更改，然后单击的映射的行**修改**。  
  
4.  在**选择目标架构**对话框，可以浏览可用的目标数据库和架构或类型的数据库和架构两个部件表示法 (database.schema) 的文本框中的名称，然后单击**确定**.  
  
5.  在目标上的更改**架构映射**选项卡。  
  
**模式的映射**  
  
-   映射到 SQL Server  
  
您可以将源数据库映射到任何目标数据库。 默认情况下映射源数据库与目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]与之有连接使用 SSMA 数据库。 是否要映射的目标数据库上不存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，然后将会有一条消息提示 **"目标中不存在的数据库和/或架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据。在同步过程中将创建它。是否要继续？"** 单击是。 同样，您可以映射到目标下不存在架构的架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]将在同步过程中创建的数据库。  
  
-   映射到 SQL Azure  
  
到连接的目标 SQL Azure 数据库或连接的目标 SQL Azure 数据库中的任何架构，可以将源数据库的映射。 如果将源架构映射到连接的目标数据库，任何非现有架构，则将会有一条消息，提示 **"架构不存在目标元数据中。在同步过程中将创建它。您想要继续吗？"** 单击是。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>还原为默认数据库和架构  
如果自定义 ASE 架构之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 架构，可以还原为默认值的映射。  
  
**若要恢复为默认数据库和架构**  
  
1.  在架构映射选项卡下选择任何行，然后单击**重置为默认值**还原为默认数据库和架构。  
  
## <a name="next-steps"></a>后续步骤  
如果想要分析的 Sybase ASE 对象转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象，你可以[创建转换报告](http://msdn.microsoft.com/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c)。 否则，你可以[转换 ASE 数据库对象定义](http://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3)到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象定义。  
  
## <a name="see-also"></a>请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
