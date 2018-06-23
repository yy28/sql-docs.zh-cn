---
title: 在使用 bcp 时指定数据格式以获得兼容性 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bulk exporting [SQL Server], compatibility
- bulk importing [SQL Server], compatibility
- compatibility [SQL Server], data formats
- data formats [SQL Server], compatibility
- bcp utility [SQL Server], compatibility
ms.assetid: cd5fc8c8-eab1-4165-9468-384f31e53f0a
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ede5c38153c30e5b7c528d6b9cd415fa739b94a0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014542"
---
# <a name="specify-data-formats-for-compatibility-when-using-bcp-sql-server"></a>在使用 bcp 时指定数据格式以获得兼容性 (SQL Server)
  本主题介绍数据格式属性、 特定于字段的提示和中的一个非 xml 格式化文件的存储按字段数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`bcp`命令。 在您大容量导出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据以便大容量导入到其他程序（例如其他数据库程序）时，理解上述概念可能会对您很有帮助。 源表中的默认数据格式（本机、字符或 Unicode）可能与其他程序所需的数据布局不兼容。如果存在不兼容，则导出数据时，必须说明数据布局。  
  
> [!NOTE]  
>  如果不熟悉导入或导出数据的数据格式，请参阅 [用于批量导入或导出的数据格式 (SQL Server)](data-formats-for-bulk-import-or-bulk-export-sql-server.md)。  
  
 **本主题内容：**  
  
-   [bcp 数据格式属性](#bcpDataFormatAttr)  
  
-   [字段特定的提示概述](#FieldSpecificPrompts)  
  
-   [将按字段数据存储在一个非 XML 格式化文件](#FieldByFieldNonXmlFF)  
  
-   [相关任务](#RelatedTasks)  
  
##  <a name="bcpDataFormatAttr"></a> bcp 数据格式属性  
 `bcp` 命令允许您按照下列数据格式属性指定数据文件中每个字段的结构：  
  
-   文件存储类型  
  
     “文件存储类型”  说明数据在数据文件中的存储方式。 可以将数据导出到数据文件为其数据库的表类型 （本机格式）、 字符表示形式 （字符格式），或为其中支持隐式转换; 任何数据类型例如，复制`smallint`作为`int`。 用户定义的数据类型将按其基类型导出。 有关详细信息，请参阅 [使用 bcp 指定文件存储类型 (SQL Server)](specify-file-storage-type-by-using-bcp-sql-server.md)。  
  
-   前缀长度  
  
     当以本机格式将数据大容量导出到数据文件时，为使文件存储空间最为紧凑，`bcp` 命令将在每个字段前面使用一个或多个字符来指示字段的长度。 这些字符称为“长度前缀字符” 。 有关详细信息，请参阅 [使用 bcp 指定数据文件中的前缀长度 (SQL Server)](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)。  
  
-   字段长度  
  
     字段长度指示以字符格式表示数据时所要求的最大字符数。 如果数据以本机格式存储，则字段长度已知。 有关详细信息，请参阅 [使用 bcp 指定字段长度 (SQL Server)](specify-field-length-by-using-bcp-sql-server.md)。  
  
-   字段终止符  
  
     对于字符数据字段，可以选择使用终止字符标记数据文件中每个字段的结尾（使用“字段终止符”）以及每行的结尾（使用“行终止符”）。 终止符是为读取数据文件的程序提供的一种方法，用于指出一个字段或行的结束位置和另一个字段或行的开始位置。 有关详细信息，请参阅 [指定字段终止符和行终止符 (SQL Server)](specify-field-and-row-terminators-sql-server.md)。  
  
##  <a name="FieldSpecificPrompts"></a> 字段特定的提示概述  
 如果交互式`bcp`命令包含**中**或**出**选项，但不还包含格式文件开关 (**-f**) 或数据格式开关 （**-n**， **-c**， **-w**，或 **-N**)，源或目标表中的每个列，该命令将为每个前面的提示打开中的属性。 在每个提示，`bcp`命令提供一个默认值基于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表列数据类型。 接受所有提示的默认值生成的结果与在命令行指定本机格式 (**-n**) 生成的结果相同。 每个提示都会显示一个用方括号括起来的默认值：[*default*]。 按 Enter 即接受显示的默认值。 若要指定与默认值不同的值，请在提示符下输入新值。  
  
### <a name="example"></a>示例  
 下面的示例使用`bcp`命令大容量导出数据从`HumanResources.myTeam`表以交互方式为`myTeam.txt`文件。 在运行该示例之前，必须创建此表。 有关该表和如何创建该表的信息，请参阅 [HumanResources.myTeam 示例表 (SQL Server)](humanresources-myteam-sample-table-sql-server.md)。  
  
 该命令指定不格式化文件，也不是数据类型，导致`bcp`，提示输入数据格式信息。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示符下输入：  
  
```  
bcp AdventureWorks.HumanResources.myTeam out myTeam.txt -T  
```  
  
 对于每列，bcp 都提示输入字段特定的值。 以下示例显示了针对表中 `EmployeeID` 和 `Name` 两个字段的提示，并为每列提供了建议的默认文件存储类型（本机格式）。 `EmployeeID` 和 `Name` 列的前缀长度分别为 0 和 2。 用户指定英文逗号 (`,`) 作为每个字段的终止符。  
  
 `Enter the file storage type of field EmployeeID [smallint]:`  
  
 `Enter prefix-length of field EmployeeID [0]:`  
  
 `Enter field terminator [none]:,`  
  
 `Enter the file storage type of field Name [nvarchar]:`  
  
 `Enter prefix length of field Name [2]:`  
  
 `Enter field terminator [none]:,`  
  
 `.`  
  
 `.`  
  
 `.`  
  
 依次针对每个表列显示以上提示（根据需要）。  
  
##  <a name="FieldByFieldNonXmlFF"></a> 将逐个字段数据存储在非 XML 格式化文件中  
 在所有的表指定了列，`bcp`命令提示您生成 （可选） 将存储的按字段信息刚刚提供 （请参阅前面的示例中） 的非 XML 格式化文件。 如果选择生成格式化文件，则可以随时从表中导出数据，也可以将结构类似的数据导入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  可以使用格式化文件将数据文件中的数据大容量导入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例中，也可以使用格式化文件从表中大容量导出数据，而无需重新指定格式。 有关详细信息，请参阅 [用来导入或导出数据的格式化文件 (SQL Server)](format-files-for-importing-or-exporting-data-sql-server.md)。  
  
 以下示例创建一个名为 `myFormatFile.fmt` 的非 XML 格式化文件：  
  
 `Do you want to save this format information in a file? [Y/n] y`  
  
 `Host filename: [bcp.fmt]myFormatFile.fmt`  
  
 该格式化文件的默认名称为 bcp.fmt，但您可以指定其他文件名。  
  
> [!NOTE]  
>  对于使用单一数据格式（如字符或本机格式）作为文件存储类型的数据文件，可以快速创建格式化文件，而无需使用 **格式** 选项导出或导入数据。 这种方法的优点在于操作简单以及允许用户创建 XML 格式化文件或非 XML 格式化文件。 有关详细信息，请参阅 [创建格式化文件 (SQL Server)](create-a-format-file-sql-server.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [使用 bcp 指定文件存储类型 (SQL Server)](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
-   [使用 bcp 指定数据文件中的前缀长度 (SQL Server)](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [使用 bcp 指定字段长度 (SQL Server)](specify-field-length-by-using-bcp-sql-server.md)  
  
-   [指定字段终止符和行终止符 (SQL Server)](specify-field-and-row-terminators-sql-server.md)  
  
## <a name="related-content"></a>相关内容  
 无。  
  
## <a name="see-also"></a>请参阅  
 [批量导入和导出数据 (SQL Server)](bulk-import-and-export-of-data-sql-server.md)   
 [用于批量导入或导出的数据格式 (SQL Server)](data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)  
  
  
