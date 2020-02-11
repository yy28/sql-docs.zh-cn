---
title: ODBC Visual FoxPro 安装程序对话框 |Microsoft Docs
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
ms.openlocfilehash: d9aa8954cd42ac715b3e6e67e0b0add69d07a570
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915665"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro 设置对话框
利用 " **ODBC Visual Foxpro 设置**" 对话框，您可以添加或更改 Visual FoxPro 数据源。  
  
 若要下载驱动程序，请参阅[Visual FOXPRO ODBC 驱动程序下载站点](https://go.microsoft.com/fwlink/?LinkId=121318)。  
  
## <a name="dialog-box-options"></a>对话框选项  
 **数据源名称**  
 键入要用于数据源的名称。  
  
 **说明**  
 键入数据源的说明。  
  
 **数据库类型**  
 允许您选择要将数据源连接到的数据库的类型。  
  
 **Visual FoxPro 数据库（。DBC**  
 指定数据源连接到 Visual FoxPro[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)（dbc 文件），并连接到数据库中的所有表和本地视图。  
  
 **可用表目录**  
 指定数据源连接到[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目录。 ODBC 目录函数（如[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)或[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)）将忽略相同目录中的任何[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)表。 可以通过使用通过[SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)和[SQLEXECDIRECT](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)发送的 SQL SELECT 语句来访问数据库表。  
  
 **通道**  
 显示数据库的路径和名称，或数据源连接到的可用表的目录。  
  
 **“浏览”**  
 使您能够在您的系统和网络中搜索您要将数据源连接到的数据库或目录。  
  
 **选项**  
 展开对话框，以便可以设置 Visual FoxPro ODBC 驱动程序选项。  
  
## <a name="driver"></a>驱动程序  
 **排序顺序**  
 字段的排序顺序。 默认序列反映了你的操作系统的语言版本支持的序列。 有关支持的排序规则的列表，请参阅[设置整理](../../odbc/microsoft/set-collate-command.md)。  
  
 **排他**  
 如果选中此复选框，则在使用数据源访问数据时，驱动程序将独占打开 Visual FoxPro 数据库。 当数据库以独占方式打开时，其他用户无法访问数据库或数据库中的表。 独占打开的数据库中的表将作为共享打开。 若要以独占方式打开表，请使用 "[设置独占](../../odbc/microsoft/set-exclusive-command.md)" 命令。 当**数据库类型**设置为 "**可用表目录**" 时，此复选框处于禁用状态。  
  
 **Null**  
 确定通过 ALTER TABLE 和 CREATE TABLE 创建的列是否允许 null 值。 如果将 Null 设置为 ON，则 INSERT SQL 会将 Null 值插入到不包含在 INSERT SQL .。。VALUE 子句。 如果 Null 为 OFF，则插入空白。 还可以通过传递的连接字符串来控制此选项，如以下代码所示：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **删除**  
 确定是否返回标记为删除的行。 还可以通过传递的连接字符串来控制此选项，如以下代码所示：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **在后台提取数据**  
 确定是在后台提取记录（连续获取）还是应用程序将等待，直到提取结果集中的所有记录。
