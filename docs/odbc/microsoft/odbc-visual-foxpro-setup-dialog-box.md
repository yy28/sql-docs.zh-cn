---
title: ODBC Visual FoxPro 安装程序对话框中 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d9a21f344687878d1a5b63073f1e23078386868
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro 安装程序对话框
**ODBC Visual FoxPro 安装**对话框中，可以添加或更改 Visual FoxPro 数据源。  
  
 若要下载驱动程序，请参阅[Visual FoxPro ODBC 驱动程序下载站点](http://go.microsoft.com/fwlink/?LinkId=121318)。  
  
## <a name="dialog-box-options"></a>对话框选项  
 **数据源名称**  
 键入你想要使用的数据源的名称。  
  
 **Description**  
 键入数据源的说明。  
  
 **数据库类型**  
 允许你选择你想要连接到你的数据源的数据库的类型。  
  
 **Visual FoxPro 数据库 (。DBC)**  
 指定数据源连接到 Visual FoxPro[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)（.dbc 文件） 和访问所有表和数据库中的本地视图。  
  
 **可用表目录**  
 指定数据源连接到的目录[释放表](../../odbc/microsoft/visual-foxpro-terminology.md)。 任何[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)位于同一目录中的表，将忽略 ODBC 目录函数如[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)或[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)。 可以使用通过发送的 SQL SELECT 语句访问数据库表[SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)和[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)。  
  
 **路径**  
 显示的路径和用于数据库或数据源连接到的可用表的目录的名称。  
  
 **浏览**  
 使您可以搜索您的系统和网络中的数据库或你想要连接的数据源的目录。  
  
 **Options**  
 展开对话框中，以便您可以设置 Visual FoxPro ODBC 驱动程序选项。  
  
## <a name="driver"></a>驱动程序  
 **排序规则序列**  
 字段的排序顺序的序列。 默认的序列反映语言版本的操作系统支持的序列。 有关支持的排序规则序列的列表，请参阅[设置 COLLATE](../../odbc/microsoft/set-collate-command.md)。  
  
 **排他**  
 选中此复选框后，该驱动程序将打开 Visual FoxPro 数据库，以独占方式访问数据源使用的数据时。 当以独占方式打开该数据库，其他用户无法访问数据库或数据库中的表。 为 SHARED 打开以独占方式打开的数据库中的表。 若要以独占方式打开表，请使用[独占设置](../../odbc/microsoft/set-exclusive-command.md)命令。 禁用此复选框时**数据库类型**设置为**可用表目录**。  
  
 **Null**  
 确定是否使用 ALTER TABLE 和 CREATE TABLE 创建列允许 null 值。 如果你设置为 Null ON，插入 – SQL 会将 null 值插入到插入-SQL 中不包含任何列...VALUE 子句。 如果为关闭 Null，则将插入空白。 你还可以控制此选项通过传递的连接字符串，如以下代码所示：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **删除**  
 确定是否返回标记为已删除的行。 你还可以控制此选项通过传递的连接字符串，如以下代码所示：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **在后台提取数据**  
 确定是否将在后台 （渐进式提取） 提取记录或者你的应用程序将等待，直到提取中的结果集的所有记录。
