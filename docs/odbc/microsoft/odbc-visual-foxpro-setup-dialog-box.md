---
title: ODBC Visual FoxPro 设置对话框 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e2d83f77f8bb9227daab996e425d1880d1bfabd
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51674408"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro 设置对话框
**ODBC Visual FoxPro 设置**对话框中，您可以添加或更改 Visual FoxPro 数据源。  
  
 若要下载驱动程序，请参阅[Visual FoxPro ODBC 驱动程序下载站点](https://go.microsoft.com/fwlink/?LinkId=121318)。  
  
## <a name="dialog-box-options"></a>对话框选项  
 **数据源名称**  
 键入你想要使用的数据源的名称。  
  
 **Description**  
 键入数据源的说明。  
  
 **数据库类型**  
 可以选择你想要连接到你的数据源的数据库的类型。  
  
 **Visual FoxPro 数据库 (。DBC)**  
 指定数据源连接到 Visual FoxPro[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)（.dbc 文件） 以及所有表和数据库中的本地视图。  
  
 **可用表目录**  
 指定数据源连接到的目录[免费表](../../odbc/microsoft/visual-foxpro-terminology.md)。 任何[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)相同的目录中的表，将忽略 ODBC 目录函数如[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)或[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)。 可以使用通过发送的 SQL SELECT 语句访问数据库表[SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)并[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)。  
  
 **路径**  
 显示的路径和名称的数据库或数据源连接的可用表的目录。  
  
 **“浏览”**  
 使您可以搜索您的系统和网络中的数据库或你想要连接到数据源的目录。  
  
 **选项**  
 展开此对话框，以便您可以设置 Visual FoxPro ODBC 驱动程序选项。  
  
## <a name="driver"></a>驱动程序  
 **对序列进行排序**  
 字段的排序顺序的序列。 默认序列反映您的操作系统语言版本支持的序列。 有关受支持的排序规则序列的列表，请参阅[设置 COLLATE](../../odbc/microsoft/set-collate-command.md)。  
  
 **排他**  
 选中此复选框，该驱动程序将访问使用数据源的数据时以独占方式打开的 Visual FoxPro 数据库。 以独占方式打开该数据库时，其他用户无法访问数据库或数据库中的表。 以独占方式打开的数据库中的表，则打开为共享。 若要以独占方式打开表，请使用[独占设置](../../odbc/microsoft/set-exclusive-command.md)命令。 禁用此复选框时**数据库类型**设置为**免费表目录**。  
  
 **Null**  
 确定是否使用 ALTER TABLE 和 CREATE TABLE 创建的列允许 null 值。 如果设置为 Null ON 时，INSERT-SQL 将 null 值插入到插入-SQL 中不包含任何列...VALUE 子句。 如果 Null 为 OFF，则将插入空白。 此外可以控制此选项在传递的连接字符串，如以下代码所示：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **已删除**  
 确定是否返回标记为已删除的行。 此外可以控制此选项在传递的连接字符串，如以下代码所示：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **后台提取数据**  
 确定是否在后台 （渐进式提取） 中提取的记录，或者你的应用程序将等待，直到提取中的结果集的所有记录。
