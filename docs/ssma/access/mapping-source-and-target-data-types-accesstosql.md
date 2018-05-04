---
title: 映射源和目标数据类型 (AccessToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- customizing data type mappings
- data types, mapping
- mapping, data types
- source data types
- target data types
ms.assetid: b362a075-16e7-423f-b63f-e1e9f02844a9
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3bb6bd72d6b20ef207653b904607a9df942c2858
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-source-and-target-data-types-accesstosql"></a>映射源和目标数据类型 (AccessToSQL)
访问数据库类型与不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库类型。 当转换到的访问数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象，你必须指定如何将访问的数据类型映射[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您可以接受默认数据类型映射，也可以自定义映射，如以下过程中所示。  
  
## <a name="default-mappings"></a>默认映射  
SSMA 具有一组默认的数据类型映射。 有关默认映射的列表，请参阅[（类型映射） 的项目设置](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655)。  
  
## <a name="customizing-data-type-mappings"></a>自定义数据类型映射  
通过使用**项目设置**对话框中，你可以自定义类型的所有数据库和项目中的数据库对象的映射方式。 一个项目的类型映射适用于所有数据库和不具有自定义类型映射的数据库对象。  
  
你还可以自定义级别的数据库或表的数据类型映射。  
  
以下过程说明如何将在项目、 数据库或数据库对象级别的数据类型映射。  
  
**若要将数据类型映射**  
  
1.  若要自定义整个项目的数据类型映射，请打开**项目设置**对话框中：  
  
    1.  上**工具**菜单上，选择**项目设置**。  
  
    2.  在左窗格中，选择**类型映射**。  
  
        类型映射图表和按钮显示在右窗格中。  
  
    或者，若要自定义级别的数据库或表的数据类型映射，请选择数据库或表在访问元数据资源管理器窗格中：  
  
    1.  在访问元数据资源管理器窗格中，展开**访问元数据库**，然后展开**数据库**。  
  
    2.  选择你想要自定义数据类型映射的数据库或表。  
  
    3.  在右窗格中，单击**类型映射**。  
  
2.  若要添加新的映射，请执行以下操作：  
  
    1.  在类型映射窗格中，单击**添加**。  
  
    2.  在**新类型映射**对话框中，在**源类型**，选择要映射的访问的数据类型。  
  
    3.  如果类型需要的长度，通过选择指定的映射的最小和最大数据长度**从**和**到**复选框，，然后输入值。  
  
        这允许你自定义相同的数据类型的较小且更大值的数据映射。  
  
    4.  下**目标类型**，选择目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。  
  
        某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换为**框中，并依次**确定**。  
  
3.  若要编辑的数据类型映射，请执行以下操作：  
  
    1.  在类型映射窗格中，单击**编辑**。  
  
    2.  在**类型映射列表**对话框中，在**源类型**，选择要映射的访问的数据类型。  
  
    3.  如果类型需要的长度，通过选择指定的映射的最小和最大数据长度**从**和**到**复选框，，然后输入值。  
  
        这允许你自定义相同的数据类型的较小且更大值的数据映射。  
  
    4.  下**目标类型**，选择目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。  
  
        某些类型需要目标数据类型长度。 如果需要，输入中的新数据长度**替换为**框中，并依次**确定**。  
  
4.  若要删除的数据类型映射，请执行以下操作：  
  
    1.  在类型映射窗格中，选择包含你想要删除的数据类型映射的类型映射列表中的行。  
  
    2.  单击 **“删除”**。  
  
## <a name="next-steps"></a>后续步骤  
迁移过程的下一步是[将访问数据库对象转换为 SQL Server 对象](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>另请参阅  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
