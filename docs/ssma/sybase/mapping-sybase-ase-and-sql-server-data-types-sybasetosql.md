---
title: 映射 Sybase ASE 和 SQL Server 数据类型 (SybaseToSQL) |Microsoft 文档
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
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d7ab2eafaeeb355d2f3f3ecd8045b0cf3ce638ad
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>映射 Sybase ASE 和 SQL Server 数据类型 (SybaseToSQL)
Sybase 自适应 Server Enterprise (ASE) 数据库类型与不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库类型。 ASE 到的数据库对象的转换时[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象，您必须指定如何映射到的 ASE 中的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您可以接受默认数据类型映射，也可以自定义映射，如以下各节中所示。  
  
## <a name="default-mappings"></a>默认映射  
SSMA 具有一组默认的数据类型映射。 有关默认映射的列表，请参阅[项目设置&#40;类型映射&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)。  
  
## <a name="type-mapping-inheritance"></a>映射继承的类型  
你可以自定义在项目级别、 对象类别级别 （例如所有存储过程） 或对象级别的类型映射。 除非在较低级别的设置覆盖，将从较高的级别继承设置。 例如，如果您映射**smallmoney**到**money**项目级别，在项目中的所有对象将都使用此映射，除非你自定义在对象类别级别或对象级别的映射。  
  
当您查看**类型映射**SSMA，背景选项卡上使用了彩色编码以显示继承的类型映射。 类型映射的背景为黄色任何继承的类型映射和为在当前级别指定任何映射的空白。  
  
## <a name="customizing-data-type-mappings"></a>自定义数据类型映射  
以下过程说明如何将在项目、 数据库或对象级别的数据类型映射。  
  
**若要将数据类型映射**  
  
1.  若要自定义整个项目的数据类型映射，请打开**项目设置**对话框中：  
  
    1.  上**工具**菜单上，选择**项目设置**。  
  
    2.  在左窗格中，选择**类型映射**。  
  
        类型映射图表和按钮显示在右窗格中。  
  
    或者，若要自定义数据类型映射在数据库、 表、 视图或存储的过程级别，选择数据库、 对象类别或对象 Sybase 元数据资源管理器中：  
  
    1.  Sybase 元数据资源管理器中选择的文件夹或你想要自定义的对象。  
  
    2.  在右窗格中，单击**类型映射**选项卡。  
  
2.  若要添加新的映射，请执行以下操作：  
  
    1.  单击 **“添加”**。  
  
    2.  下**源类型**，选择要映射的 ASE 数据类型。  
  
    3.  如果类型需要的长度，指定在映射的最小数据长度**从**框中，并指定为在映射的最大数据长度**到**框。  
  
        这允许你自定义相同的数据类型的较小且更大值的数据映射。  
  
    4.  下**目标类型**，选择目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据类型。  
  
        某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换**框。  
  
    5.  单击 **“确定”**。  
  
3.  若要编辑的数据类型映射，请执行以下操作：  
  
    1.  单击 **“编辑”**。  
  
    2.  下**源类型**，选择要映射的 ASE 数据类型。  
  
    3.  如果类型需要的长度，指定在映射的最小数据长度**从**框中，并指定为在映射的最大数据长度**到**框。  
  
        这允许你自定义相同的数据类型的较小且更大值的数据映射。  
  
    4.  下**目标类型**，选择目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据类型。  
  
        某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换**框中，并依次**确定**。  
  
4.  若要删除的自定义数据类型映射，请执行以下操作：  
  
    1.  包含你想要删除的数据类型映射的类型映射列表中选择行。  
  
    2.  单击 **“删除”**。  
  
        无法删除继承的映射。 但是，通过上的特定对象或对象类别的自定义映射中重写继承的映射。  
  
## <a name="next-steps"></a>后续步骤  
迁移过程的下一步是为[创建评估报表](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c)或[转换 Sybase ASE 的数据库对象添加到 SQL Server 或 SQL Azure 语法](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3)。 如果创建了一个评估报告，Sybase ASE 对象将自动转换此评估过程。  
  
## <a name="see-also"></a>另请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server 的 Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
