---
title: 列映射（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c1d381ec773499fdcf018375c7a51740880d3d9b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436784"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>列映射（SQL Server 导入和导出向导）
  使用 "**列映射**" 对话框可以编辑转换参数。  
  
> [!NOTE]  
>  如果选中了“表复制”选项，则不必复制表中的所有列。 **\<ignore>** 对于要跳过的列，请在此对话框的 "**目标**" 列中选择。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解用于启动向导的选项以及成功运行向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>选项  
 **Source**  
 标识所选的源表、视图或查询。  
  
 **目标**  
 标识所选的目标表、视图或查询。  
  
 **创建目标表/文件**  
 指定如果目标表不存在是否创建目标表。  
  
 **删除目标表/文件中的行**  
 指定在加载新数据之前是否清除现有表的数据。  
  
 **向目标表/文件中追加行**  
 指定是否将新数据追加到现有表的已存在数据中。  
  
 **编辑 SQL**  
 使用 "**创建表 SQL 语句**" 对话框中的默认语句，或根据您的目的修改它。 如果要修改此语句，还必须对表映射进行相关更改。  
  
 **删除并重新创建目标表**  
 选择此选项可以覆盖目标表。 只有在使用该向导创建目标表时，该选项才可用。 如果保存的是向导创建的包，则只可以删除并重新创建目标表，然后再次运行该包。  
  
 **启用标识插入**  
 选择此选项可以将源数据中的现有标识值插入到目标表中的标识列。 默认情况下，不允许对目标标识列执行此操作。  
  
 **映射**  
 显示数据源映射中的每个列如何映射到目标中列。  
  
 此列表包含以下列：  
  
 **Source**  
 查看可以为其设置转换参数的各个源列。  
  
 **目标**  
 指定在复制操作期间是否忽略列。 **\<ignore>** 对于要跳过的列，请在此列中进行选择，以便只复制列的子集。 在映射列之前，必须忽略所有不会被映射的列。  
  
 **Type**  
 为列选择数据类型。  
  
 **可以为 Null**  
 指定列是否允许 Null 值。  
  
 **大小**  
 指定列中的字符数。  
  
 **精度**  
 指定所显示数据的精度（指数字的位数）。  
  
 **缩放**  
 指定所显示数据的小数位数（指小数点后的位数）。  
  
  
