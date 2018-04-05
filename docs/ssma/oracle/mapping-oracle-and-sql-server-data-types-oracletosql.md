---
title: 映射 Oracle 和 SQL Server 数据类型 (OracleToSQL) |Microsoft 文档
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 8984f279cb6a42d057093f048a29149a7be2d981
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>映射 Oracle 和 SQL Server 数据类型 (OracleToSQL)
Oracle 数据库类型与不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库类型。 当转换到的 Oracle 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象，你必须指定如何将从到 Oracle 数据类型映射[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您可以接受默认数据类型映射，也可以自定义映射，如以下各节中所示。  
  
## <a name="default-mappings"></a>默认映射  
SSMA 具有一组默认的数据类型映射。 有关默认映射的列表，请参阅[项目设置 &#40;类型映射 &#41;&#40; OracleToSQL &#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
## <a name="type-mapping-inheritance"></a>映射继承的类型  
你可以自定义在项目级别、 对象类别级别 （例如所有存储过程） 或对象级别的类型映射。 除非重写，则在较低级别，将从较高的级别继承设置。 例如，如果您映射**smallmoney**到**money**项目级别，在项目中的所有对象将都使用此映射，除非你自定义级别的对象或类别的映射。  
  
当您查看**类型映射**SSMA，背景选项卡上使用了彩色编码以显示继承的类型映射。 类型映射的背景为黄色任何继承的类型映射和为在当前级别指定任何映射的空白。  
  
## <a name="customizing-data-type-mappings"></a>自定义数据类型映射  
下面的过程演示如何将在项目、 数据库或对象级别的数据类型映射：  
  
**若要将数据类型映射**  
  
1.  若要自定义整个项目的数据类型映射，请打开**项目设置**对话框中：  
  
    1.  上**工具**菜单上，选择**项目设置**。  
  
    2.  在左窗格中，选择**类型映射**。  
  
        类型映射图表和按钮显示在右窗格中。  
  
    或者，若要自定义数据类型映射在数据库、 表、 视图或存储的过程级别，选择数据库、 对象类别或对象在 Oracle 元数据资源管理器：  
  
    1.  在 Oracle 元数据资源管理器中，选择文件夹或对象以自定义。  
  
    2.  在右窗格中，单击**类型映射**选项卡。  
  
2.  若要添加新的映射，请执行以下操作：  
  
    1.  单击 **“添加”**。  
  
    2.  下**源类型**，选择要映射的 Oracle 数据类型。  
  
    3.  如果类型需要的长度，指定在映射的最小数据长度**从**框和中的最大数据长度**到**框。  
  
        这允许你自定义相同的数据类型的较小且更大值的数据映射。  
  
    4.  下**目标类型**，选择目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。  
  
        某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换**框。  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
3.  若要修改的数据类型映射，请执行以下操作：  
  
    1.  单击 **“编辑”**。  
  
    2.  下**源类型**，选择要映射的 Oracle 数据类型。  
  
    3.  如果类型需要的长度，指定在映射的最小数据长度**从**框和中的最大数据长度**到**框。  
  
        这允许你自定义相同的数据类型的较小且更大值的数据映射。  
  
    4.  下**目标类型**，选择目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。  
  
        某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换**框中，然后[!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
4.  若要删除的自定义数据类型映射，请执行以下操作：  
  
    1.  包含你想要删除的数据类型映射的类型映射列表中选择行。  
  
    2.  单击 **“删除”**。  
  
        无法删除继承的映射。 但是，通过上的特定对象或对象类别的自定义映射中重写继承的映射。  
  
## <a name="next-steps"></a>Next Steps  
迁移过程的下一步是为[创建评估报表](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357)或[Oracle 数据库对象转换为 SQL Server 语法](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272)。 如果创建了一个评估报告，Oracle 对象将自动转换此评估过程。  
  
## <a name="see-also"></a>另请参阅  
[将 Oracle 数据库迁移到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
