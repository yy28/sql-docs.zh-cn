---
title: "映射 MySQL 和 SQL Server 数据类型 (MySQLToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping, customize data type mapping
- Mapping, Type mapping
ms.assetid: 14f98054-13b4-4231-a6b0-2452f3b9941d
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3dd2adf0b8f6379bd11dc80de4cc2aedf5b3c102
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>将 MySQL 和 SQL Server 数据类型 (MySQLToSQL) 映射
MySQL 数据库类型与不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 数据库类型。 当转换到的 MySQL 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象，你必须指定如何将从到 MySQL 的数据类型映射[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您可以接受默认数据类型映射，也可以自定义映射，如以下过程中所示。  
  
## <a name="default-mappings"></a>默认映射  
SSMA 具有一组默认的数据类型映射。 有关默认映射的列表，请参阅[项目设置 &#40;类型映射 &#41;&#40;MySQLToSQL &#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
## <a name="type-mapping-inheritance"></a>映射继承的类型  
你可以自定义在项目级别、 对象类别级别 （例如所有存储过程） 或对象级别的类型映射。 除非重写，则在较低级别，将从较高的级别继承设置。 例如，如果您映射**smallint**到**int**项目级别，在项目中的所有对象将都使用此映射，除非你自定义级别的对象或类别的映射。  
  
当您查看**类型映射**SSMA，背景选项卡上使用了彩色编码以显示继承的类型映射。 类型映射的背景为黄色任何继承的类型映射和为在当前级别指定任何映射的空白。  
  
## <a name="customizing-data-type-mappings"></a>自定义数据类型映射  
  
-   **映射数据类型：**  
  
    下面的过程演示如何将在项目、 数据库或数据库对象级别的数据类型映射：  
  
    1.  若要自定义整个项目的数据类型映射，请打开**项目设置**对话框。 在工具菜单中，选择**项目设置**。  
  
        在左窗格中，选择**类型映射**。 类型映射图表和按钮显示在右窗格中。  
  
    2.  要自定义级别的数据库或表的数据类型映射，请在 MySQL 元数据资源管理器中选择数据库或表。 在 MySQL 元数据资源管理器中，选择文件夹或对象以自定义。  
  
        在右窗格中，单击**类型映射**。  
  
-   **若要添加新的映射，请执行以下操作：**  
  
    1.  在类型映射窗格中，单击**添加**。  
  
    2.  在新建键入映射对话框中下,**源类型**，选择要映射的 MySQL 数据类型。  
  
    3.  如果类型需要的长度，通过选择指定的映射的最小和最大数据长度**从**和**到**复选框，，然后输入值。  
  
    4.  这允许你自定义相同的数据类型的较小且更大值的数据映射。 下**目标类型**，选择的目标 SQL Server 或 SQL Azure 数据类型。  
  
        1.  某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换为**框中，并依次**确定**。  
  
        2.  某些类型需要目标数据类型**精度**和**缩放**。 如果需要，输入新的精度和向内缩放**替换为**框中，并依次**确定**。  
  
-   **若要编辑的类型映射，请执行以下操作：**  
  
    1.  在类型映射窗格中，单击**编辑**。  
  
    2.  中的类型映射列表对话框中下,**源类型**，选择要映射的 MySQL 数据类型。  
  
    3.  如果类型需要的长度，通过选择指定的映射的最小和最大数据长度**从**和**到**复选框，，然后输入值。  
  
    这允许你自定义相同的数据类型的较小且更大值的数据映射。 下**目标类型**，选择的目标 SQL Server 或 SQL Azure 数据类型。  
  
    1.  某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换为**框中，并依次**确定**。  
  
    2.  某些类型需要目标数据类型**精度**和**缩放**。 如果需要，输入新的精度和向内缩放**替换为**框中，并依次**确定**。  
  
-   **若要删除的数据类型映射，请执行以下操作：**  
  
    1.  在类型映射窗格中，选择包含你想要删除的数据类型映射的类型映射列表中的行。  
  
    2.  单击 **“删除”**。  
  
## <a name="next-step"></a>下一步  
迁移过程的下一步是为[创建评估报表](http://msdn.microsoft.com/en-us/2a56a003-3b0f-453a-963c-00c9e40933ec)或[转换 MySQL 数据库对象，为 SQL Server 或 SQL Azure 语法](http://msdn.microsoft.com/en-us/ac21850b-fb32-4704-9985-5759b7c688c7)。 如果你创建报表，MySQL 对象将自动转换此评估过程。  
  
## <a name="see-also"></a>另請參閱  
[将 MySQL 数据库迁移到 SQL Server 的 Azure SQL DB &#40;MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

