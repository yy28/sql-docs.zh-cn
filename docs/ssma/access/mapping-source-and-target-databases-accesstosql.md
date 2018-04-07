---
title: 映射源和目标数据库 (AccessToSQL) |Microsoft 文档
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
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
- database schemas
- mapping, databases
- schemas, mapping to
- schemas, SQL Azure
- schemas, SQL Server
- source database
- target database
ms.assetid: 69bee937-7b2c-49ee-8866-7518c683fad4
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eed81b1bf2d9f3f2e70f30a6744c4d7ad9bf33d3
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>映射源和目标数据库 (AccessToSQL)
当您连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，你需要指定用于迁移的目标数据库。 如果你有多个访问数据库可以将它们映射到多个[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库 （或架构） 或连接的 SQL Azure 数据库下的多个架构。  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>SQL Server 或 SQL Azure 数据库架构  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库使用的架构的概念来进行分隔为逻辑组的数据库中的对象。 例如，是库数据库可以使用名为的三个架构**丛书**，**音频**，和**视频**相互分隔书籍，音频和视频对象。 默认情况下，访问数据库映射到**master**数据库和**dbo**架构中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和连接的数据库和**dbo** SQL Azure 中的架构。  
  
除非你自定义每个访问数据库之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库和架构，SSMA 将迁移所有的架构和数据与访问数据库，到映射的默认数据库关联。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目标数据库和架构  
SSMA 方式可以将映射到每个访问数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库和架构。 以下过程描述如何自定义每个数据库的映射。  
  
**若要修改目标数据库和架构**  
  
1.  在访问元数据资源管理器窗格中，选择**访问元数据**。  
  
    你选择时，可能也是可用架构映射**数据库**节点或任何数据库节点。 为所选对象自定义架构映射列表。  
  
2.  在右窗格中，单击**架构映射**选项卡。  
  
    你将看到一个包含访问表数据库名称和其相应 ssNoVersion 或 Sql Azure 架构。 目标架构中由两部分表示法 (database.schema) 表示。  
  
3.  选择包含你想要自定义，然后单击的映射的行**修改**。  
  
4.  在**选择目标架构**对话框中，你可以浏览可用的目标数据库和架构或类型的数据库和架构中由两部分表示法 (database.schema) 的文本框的名称，然后单击**确定**。  
  
**映射模式**  
  
-   将映射到 SQL Server  
  
可以将源数据库映射到任何目标数据库。 默认情况下映射源数据库到目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]具有与其连接使用 SSMA 数据库。 如果要映射的目标数据库上不存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，则系统将提示你使用的消息**"目标中不存在的数据库和/或架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据。它会在同步期间创建。是否要继续？"** 单击是。 同样，可以架构映射到在目标下不存在架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库将在同步期间创建的。  
  
-   将映射到 SQL Azure  
  
你可以将源数据库映射到已连接的目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库或到连接的目标中的任何架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。 如果将源架构映射到已连接的目标数据库在任何非现有架构，则系统将提示您提供一条消息**"架构中不存在目标元数据。它会在同步期间创建。你想要继续吗？"**单击是。  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>还原为初始数据库和架构  
如果你自定义的 Access 数据库之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库和架构，你可以还原到指定连接到数据库的映射[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
**若要重置为默认数据库和架构**  
  
1.  在架构映射的选项卡上，选择任何行，然后单击**重置为默认**若要还原到的默认数据库和架构。  
  
## <a name="next-step"></a>下一步  
迁移过程的下一步是[转换数据库对象](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>另请参阅  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
