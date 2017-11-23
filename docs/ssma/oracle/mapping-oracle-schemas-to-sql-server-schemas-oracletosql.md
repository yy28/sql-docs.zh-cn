---
title: "将 Oracle 架构映射到 SQL Server 架构 (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: 8ab69b6f55033e8d6687c0bc0b5e6cf9bfdf1417
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>将 Oracle 架构映射到 SQL Server 架构 (OracleToSQL)
在 Oracle 中，每个数据库都有一个或多个架构。 默认情况下，SSMA 将迁移到 Oracle 架构中的所有对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]架构名为的数据库。 但是，你可以自定义 Oracle 架构之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。  
  
## <a name="oracle-and-sql-server-schemas"></a>Oracle 和 SQL Server 架构  
Oracle 数据库包含架构。 实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]包含多个数据库，其中每个可以有多个架构。  
  
架构的 Oracle 概念映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库和一个其架构的概念。 例如，Oracle 可能具有名为的架构**HR**。 实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]可能具有一个名为数据库**HR**，并且该数据库中的架构。 一个架构**dbo** （或数据库所有者） 架构。 默认情况下，Oracle 架构**HR**将映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库和架构**HR.dbo**。 SSMA 是指[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库和架构的组合为一个架构。  
  
你可以修改 Oracle 之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]架构。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目标数据库和架构  
在 SSMA，可以将 Oracle 架构映射到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]架构。  
  
**若要修改的数据库和架构**  
  
1.  在 Oracle 元数据资源管理器中，选择**架构**。  
  
    **架构映射**时选择单独的数据库，，可能也是可用选项卡**架构**文件夹或单个架构。 中的列表**架构映射**选项卡上自定义的所选对象。  
  
2.  在右窗格中，单击**架构映射**选项卡。  
  
    你将看到的所有 Oracle 架构，跟目标值的列表。 此目标中，表示在由两部分表示法 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象和数据将迁移。  
  
3.  选择包含你想要更改，然后单击的映射的行**修改**。  
  
    在**选择目标架构**对话框中，你可以浏览可用的目标数据库和架构或类型的数据库和架构中由两部分表示法 (database.schema) 的文本框的名称，然后单击**确定**。  
  
4.  目标上的更改**架构映射**选项卡。  
  
**映射模式**  
  
-   将映射到 SQL Server  
  
可以将源数据库映射到任何目标数据库。 默认情况下映射源数据库到目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]具有与其连接使用 SSMA 数据库。 要映射的目标数据库是否不存在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，则系统将提示你使用的消息**"目标中不存在的数据库和/或架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据。它会在同步期间创建。是否要继续？"** 单击是。 同样，可以架构映射到在目标下不存在架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库将在同步期间创建的。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>还原为默认数据库和架构  
如果你自定义的 Oracle 架构之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]架构，你可以还原回默认值的映射。  
  
**若要还原到的默认数据库和架构**  
  
1.  在架构映射的选项卡上，选择任何行，然后单击**重置为默认**若要还原到的默认数据库和架构。  
  
## <a name="next-steps"></a>后续步骤  
如果你想要分析的 Oracle 对象转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象，你可以[创建转换报表](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357)。 否则，你可以[转换 Oracle 数据库对象定义](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272)到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象定义。  
  
## <a name="see-also"></a>另请参阅  
[连接到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[将 Oracle 数据库迁移到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
