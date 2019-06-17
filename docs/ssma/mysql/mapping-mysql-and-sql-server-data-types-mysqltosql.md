---
title: 映射 MySQL 和 SQL Server 数据类型 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, customize data type mapping
- Mapping, Type mapping
ms.assetid: 14f98054-13b4-4231-a6b0-2452f3b9941d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ffe475b53048a97f878bfad1d8bef68d6fb3cfc6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312513"
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>映射 MySQL 和 SQL Server 数据类型 (MySQLToSQL)
MySQL 数据库类型不同于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 数据库类型。 转换到 MySQL 数据库对象时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象，您必须指定如何将数据类型从 mysql 迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 可以接受默认数据类型映射，也可以自定义映射，如下面的过程中所示。  
  
## <a name="default-mappings"></a>默认映射  
SSMA 具有一组默认的数据类型映射。 有关默认映射的列表，请参阅[项目设置&#40;类型映射&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)。  
  
## <a name="type-mapping-inheritance"></a>映射继承的类型  
您可以自定义在项目级别、 对象 （例如所有存储过程） 的类别级别或对象级别的类型映射。 除非它们在较低级别重写从更高级别继承设置。 例如，如果您将映射**smallint**到**int**在项目级别，该项目中的所有对象将都使用此映射，除非你自定义对象或类别级别的映射。  
  
当您查看**类型映射**SSMA，在后台中的选项卡了彩色编码来显示继承的类型映射。 黄色表示任何继承的类型映射，并在当前级别上指定任何映射的白色背景的类型映射。  
  
## <a name="customizing-data-type-mappings"></a>自定义数据类型映射  
  
-   **若要将数据类型映射：**  
  
    下面的过程演示如何将在项目、 数据库或数据库对象级别的数据类型映射：  
  
    1.  若要自定义整个项目的数据类型映射，请打开**项目设置**对话框。 在工具菜单上选择**项目设置**。  
  
        在左窗格中，选择**类型映射**。 类型映射表和按钮显示在右窗格中。  
  
    2.  要自定义数据库或表级别的数据类型映射，请在 MySQL 元数据资源管理器中选择数据库或表。 在 MySQL 元数据资源管理器中，选择要自定义对象的文件夹。  
  
        在右窗格中，单击**类型映射**。  
  
-   **若要添加新的映射，请执行以下操作：**  
  
    1.  在类型映射窗格中，单击**添加**。  
  
    2.  在新建中键入映射对话框下**源类型**，选择要映射的 MySQL 数据类型。  
  
    3.  如果类型要求长度，通过选择来指定映射的最小和最大数据长度**从**并**到**复选框，，然后输入值。  
  
    4.  这允许您自定义的相同的数据类型的更小且更大值的数据映射。 下**目标类型**，选择目标 SQL Server 或 SQL Azure 的数据类型。  
  
        1.  某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换为**框中，然后依次**确定**。  
  
        2.  某些类型需要的目标数据类型**精度**并**规模**。 如有必要，输入新的精度和缩小**替换为**框中，然后依次**确定**。  
  
-   **若要编辑类型映射，请执行以下操作：**  
  
    1.  在类型映射窗格中，单击**编辑**。  
  
    2.  中的类型映射列表对话框的下**源类型**，选择要映射的 MySQL 数据类型。  
  
    3.  如果类型要求长度，通过选择来指定映射的最小和最大数据长度**从**并**到**复选框，，然后输入值。  
  
    这允许您自定义的相同的数据类型的更小且更大值的数据映射。 下**目标类型**，选择目标 SQL Server 或 SQL Azure 的数据类型。  
  
    1.  某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换为**框中，然后依次**确定**。  
  
    2.  某些类型需要的目标数据类型**精度**并**规模**。 如有必要，输入新的精度和缩小**替换为**框中，然后依次**确定**。  
  
-   **若要删除的数据类型映射，请执行以下操作：**  
  
    1.  在类型映射窗格中，选择包含你想要删除的数据类型映射的类型映射列表中的行。  
  
    2.  单击 **“删除”** 。  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是为[创建评估报告](assessing-mysql-databases-for-conversion-mysqltosql.md)或[到 SQL Server 或 SQL Azure 语法转换 MySQL 数据库对象](converting-mysql-databases-mysqltosql.md)。 如果创建报表时，会自动在评估期间转换 MySQL 对象。  
  
## <a name="see-also"></a>请参阅  
[迁移 MySQL 数据库移到 SQL Server-Azure SQL 数据库&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
