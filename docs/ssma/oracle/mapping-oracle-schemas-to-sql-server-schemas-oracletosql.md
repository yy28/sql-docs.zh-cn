---
title: Oracle 架构映射到 SQL Server 架构 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 61b706145f708e9b2e8a04ba4e7bc574c503a742
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52407859"
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>将 Oracle 架构映射到 SQL Server 架构 (OracleToSQL)
在 Oracle 中，每个数据库都有一个或多个架构。 默认情况下，SSMA 将迁移到的 Oracle 架构中的所有对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]命名的架构的数据库。 但是，自定义 Oracle 架构之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
## <a name="oracle-and-sql-server-schemas"></a>Oracle 和 SQL Server 架构  
Oracle 数据库包含的架构。 实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]包含多个数据库，其中每个可以有多个架构。  
  
Oracle 架构概念的将映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的数据库和其架构中的一个概念。 例如，Oracle 可能具有名为的架构**HR**。 实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可能有一个名为数据库**HR**，并在该数据库是架构。 一个架构**dbo** （或数据库所有者） 架构。 默认情况下，Oracle 架构**HR**将映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库和架构**HR.dbo**。 SSMA 是指[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架构数据库和架构的组合。  
  
您可以修改 Oracle 之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架构。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目标数据库和架构  
在 SSMA 中，可以将 Oracle 架构映射到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架构。  
  
**若要修改的数据库和架构**  
  
1.  在 Oracle 元数据资源管理器中，选择**架构**。  
  
    **架构映射**选项卡，也可选择单独的数据库，当**架构**文件夹或单个架构。 中的列表**架构映射**所选对象的自定义选项卡。  
  
2.  在右窗格中，单击**架构映射**选项卡。  
  
    您将看到所有 Oracle 架构后, 跟一个目标值的列表。 此目标中的两个部分表示法表示 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象和数据都迁移。  
  
3.  选择包含你想要更改，然后单击的映射的行**修改**。  
  
    在**选择目标架构**对话框，可以浏览可用的目标数据库和架构或类型的数据库和架构两个部件表示法 (database.schema) 的文本框中的名称，然后单击**确定**.  
  
4.  在目标上的更改**架构映射**选项卡。  
  
**模式的映射**  
  
-   映射到 SQL Server  
  
您可以将源数据库映射到任何目标数据库。 默认情况下映射源数据库与目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与之有连接使用 SSMA 数据库。 是否要映射的目标数据库上不存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然后将会有一条消息提示 **"目标中不存在的数据库和/或架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据。在同步过程中将创建它。是否想要继续？"** 单击是。 同样，您可以映射到目标下不存在架构的架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将在同步过程中创建的数据库。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>还原为默认数据库和架构  
如果自定义的 Oracle 架构之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架构，可以还原为默认值的映射。  
  
**若要恢复为默认数据库和架构**  
  
1.  在架构映射选项卡下选择任何行，然后单击**重置为默认值**还原为默认数据库和架构。  
  
## <a name="next-steps"></a>后续步骤  
如果想要分析的 Oracle 对象转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象，你可以[创建转换报告](assessing-oracle-schemas-for-conversion-oracletosql.md)。 否则，你可以[转换的 Oracle 数据库对象定义](converting-oracle-schemas-oracletosql.md)到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象定义。  
  
## <a name="see-also"></a>请参阅  
[连接到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[迁移的 Oracle 数据库移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
