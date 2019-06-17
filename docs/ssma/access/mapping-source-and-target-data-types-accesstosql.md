---
title: 映射源和目标数据类型 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- customizing data type mappings
- data types, mapping
- mapping, data types
- source data types
- target data types
ms.assetid: b362a075-16e7-423f-b63f-e1e9f02844a9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a32f7f321baa17dbcdaf557bb7de033422a02dbc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740975"
---
# <a name="mapping-source-and-target-data-types-accesstosql"></a>映射源和目标数据类型 (AccessToSQL)
访问数据库类型不同于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库类型。 转换到访问数据库对象时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象，您必须指定如何将数据类型从访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 可以接受默认数据类型映射，也可以自定义映射，如下面的过程中所示。  
  
## <a name="default-mappings"></a>默认映射  
SSMA 具有一组默认的数据类型映射。 有关默认映射的列表，请参阅[（类型映射） 的项目设置](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)。  
  
## <a name="customizing-data-type-mappings"></a>自定义数据类型映射  
通过使用**项目设置**对话框中，你可以自定义类型的所有数据库和项目中的数据库对象的映射方式。 一个项目的类型映射适用于所有数据库和数据库对象不具有自定义类型映射。  
  
此外可以自定义数据库或表级别的数据类型映射。  
  
以下过程说明如何将在项目、 数据库或数据库对象级别的数据类型映射。  
  
**若要将数据类型映射**  
  
1.  若要自定义整个项目的数据类型映射，请打开**项目设置**对话框：  
  
    1.  上**工具**菜单中，选择**项目设置**。  
  
    2.  在左窗格中，选择**类型映射**。  
  
        类型映射表和按钮显示在右窗格中。  
  
    或者，若要自定义数据库或表级别的数据类型映射，请选择表的数据库访问元数据资源管理器窗格中：  
  
    1.  在访问元数据资源管理器窗格中，展开**访问元数据库**，然后展开**数据库**。  
  
    2.  选择你想要自定义数据类型映射的数据库或表。  
  
    3.  在右窗格中，单击**类型映射**。  
  
2.  若要添加新的映射，请执行以下操作：  
  
    1.  在类型映射窗格中，单击**添加**。  
  
    2.  在中**新类型映射**对话框中的**源类型**，选择要映射的访问的数据类型。  
  
    3.  如果类型要求长度，通过选择来指定映射的最小和最大数据长度**从**并**到**复选框，，然后输入值。  
  
        这允许您自定义的相同的数据类型的更小且更大值的数据映射。  
  
    4.  下**目标类型**，选择目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。  
  
        某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换为**框中，然后依次**确定**。  
  
3.  若要编辑的数据类型映射，请执行以下操作：  
  
    1.  在类型映射窗格中，单击**编辑**。  
  
    2.  在中**类型映射列表**对话框中的**源类型**，选择要映射的访问的数据类型。  
  
    3.  如果类型要求长度，通过选择来指定映射的最小和最大数据长度**从**并**到**复选框，，然后输入值。  
  
        这允许您自定义的相同的数据类型的更小且更大值的数据映射。  
  
    4.  下**目标类型**，选择目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。  
  
        某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换为**框中，然后依次**确定**。  
  
4.  若要删除的数据类型映射，请执行以下操作：  
  
    1.  在类型映射窗格中，选择包含你想要删除的数据类型映射的类型映射列表中的行。  
  
    2.  单击 **“删除”** 。  
  
## <a name="next-steps"></a>后续步骤  
迁移过程中的下一步是[将访问数据库对象转换为 SQL Server 对象](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>请参阅  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
