---
title: 映射 Sybase ASE 和 SQL Server 数据类型 (SybaseToSQL) |Microsoft Docs
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
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9efd87a25802bd5610393beb4de0728807ea827d
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392944"
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>映射 Sybase ASE 和 SQL Server 数据类型 (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) 数据库类型不同于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库类型。 转换到 ASE 数据库对象时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象，必须指定如何将映射到 ASE 中的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 可以接受默认数据类型映射，也可以自定义映射，如以下各节中所示。  
  
## <a name="default-mappings"></a>默认映射  
SSMA 具有一组默认的数据类型映射。 有关默认映射的列表，请参阅[项目设置&#40;类型映射&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)。  
  
## <a name="type-mapping-inheritance"></a>映射继承的类型  
您可以自定义在项目级别、 对象 （例如所有存储过程） 的类别级别或对象级别的类型映射。 除非在较低级别重写从更高级别继承设置。 例如，如果您将映射**smallmoney**到**资金**在项目级别，该项目中的所有对象将都使用此映射，除非你自定义对象类别级别或对象级别的映射。  
  
当您查看**类型映射**SSMA，在后台中的选项卡了彩色编码来显示继承的类型映射。 黄色表示任何继承的类型映射，并在当前级别上指定任何映射的白色背景的类型映射。  
  
## <a name="customizing-data-type-mappings"></a>自定义数据类型映射  
以下过程说明如何将在项目、 数据库或对象级别的数据类型映射。  
  
**若要将数据类型映射**  
  
1.  若要自定义整个项目的数据类型映射，请打开**项目设置**对话框：  
  
    1.  上**工具**菜单中，选择**项目设置**。  
  
    2.  在左窗格中，选择**类型映射**。  
  
        类型映射表和按钮显示在右窗格中。  
  
    或者，若要自定义数据类型在数据库、 表、 视图或存储的过程级别的映射选择数据库、 对象类别或对象 Sybase 元数据资源管理器中：  
  
    1.  Sybase 元数据资源管理器中选择的文件夹或你想要自定义的对象。  
  
    2.  在右窗格中，单击**类型映射**选项卡。  
  
2.  若要添加新的映射，请执行以下操作：  
  
    1.  单击 **“添加”**。  
  
    2.  下**源类型**，选择要映射的 ASE 数据类型。  
  
    3.  如果类型要求长度，指定映射中的最小数据长度**从**，并指定映射中的最大数据长度**到**框。  
  
        这允许您自定义的相同的数据类型的更小且更大值的数据映射。  
  
    4.  下**目标类型**，选择目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的数据类型。  
  
        某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换为**框。  
  
    5.  单击“确定” 。  
  
3.  若要编辑的数据类型映射，请执行以下操作：  
  
    1.  单击 **“编辑”**。  
  
    2.  下**源类型**，选择要映射的 ASE 数据类型。  
  
    3.  如果类型要求长度，指定映射中的最小数据长度**从**，并指定映射中的最大数据长度**到**框。  
  
        这允许您自定义的相同的数据类型的更小且更大值的数据映射。  
  
    4.  下**目标类型**，选择目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的数据类型。  
  
        某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换为**框中，然后依次**确定**。  
  
4.  若要删除自定义数据类型映射，请执行以下操作：  
  
    1.  包含你想要删除的数据类型映射的类型映射列表中选择行。  
  
    2.  单击 **“删除”**。  
  
        不能删除继承的映射。 但是，由特定对象或对象类别的自定义映射中重写继承的映射。  
  
## <a name="next-steps"></a>后续步骤  
迁移过程中的下一步是为[创建评估报告](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)或[到 SQL Server 或 SQL Azure 语法转换 Sybase ASE 数据库对象](converting-sybase-ase-database-objects-sybasetosql.md)。 如果您创建评估报告，会自动在评估期间转换 Sybase ASE 对象。  
  
## <a name="see-also"></a>请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
