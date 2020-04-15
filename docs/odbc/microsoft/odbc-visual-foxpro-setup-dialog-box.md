---
title: ODBC 可视化狐狸专业设置对话框 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef7ac702a69342833c6dfffa0ffc9cdd0ac2857e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298077"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro 设置对话框
**ODBC 可视化 FoxPro 安装程序**对话框使您能够添加或更改 Visual FoxPro 数据源。  
  
 要下载驱动程序，请参阅[可视化福克斯Pro ODBC驱动程序下载网站](https://go.microsoft.com/fwlink/?LinkId=121318)。  
  
## <a name="dialog-box-options"></a>对话框选项  
 **数据源名称**  
 键入要用于数据源的名称。  
  
 **说明**  
 键入数据源的说明。  
  
 **数据库类型**  
 允许您选择要连接到数据源的数据库类型。  
  
 **可视化 FoxPro 数据库 （.DBC）**  
 指定数据源连接到 Visual FoxPro[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)（.dbc 文件） 以及数据库中的所有表和本地视图。  
  
 **可用表目录**  
 指定数据源连接到[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目录。 同一目录中的任何[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)表都将被 ODBC 目录函数（如[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)或[SQLTables）](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)忽略。 可以使用通过 SQLExecute 和[SQLExecDirect](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)发送的 SQL [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)SELECT 语句访问数据库表。  
  
 **路径**  
 显示数据库的路径和名称或数据源连接到的可用表的目录。  
  
 **浏览**  
 使您能够在系统和网络上搜索要连接到数据源的数据库或目录。  
  
 **选项**  
 展开对话框，以便可以设置 Visual FoxPro ODBC 驱动程序选项。  
  
## <a name="driver"></a>驱动程序  
 **整理序列**  
 字段排序的顺序。 默认序列反映操作系统的语言版本支持的顺序。 有关支持的整理序列的列表，请参阅[SET COLLATE](../../odbc/microsoft/set-collate-command.md)。  
  
 **排他**  
 选中此复选框后，当您使用数据源访问数据时，驱动程序将专门打开 Visual FoxPro 数据库。 在独占打开数据库时，其他用户无法访问数据库或数据库中的表。 独占打开的数据库中的表将作为 SHARED 打开。 要独占打开表，请使用[SET 独占](../../odbc/microsoft/set-exclusive-command.md)命令。 当**数据库类型**设置为**自由表目录**时，将禁用此复选框。  
  
 **Null**  
 确定使用 ALTER TABLE 和 CREATE TABLE 创建的列是否允许空值。 如果设置"空打开"，则"插入 " - SQL 将空值插入到插入 - SQL...VALUE 条款。 如果 Null 为 OFF，则插入空白。 还可以通过传递的连接字符串控制此选项，如以下代码中：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **删除**  
 确定是否返回标记为已删除的行。 还可以通过传递的连接字符串控制此选项，如以下代码中：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **在后台提取数据**  
 确定是在后台提取记录（逐行提取），还是应用程序将等待结果集中的所有记录被提取。
