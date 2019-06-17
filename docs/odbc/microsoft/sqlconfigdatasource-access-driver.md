---
title: SQLConfigDataSource (Access Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd626d476bf1c4ac8b4f83f397584c367299904f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62665402"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource（Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函数，用于添加、 修改或删除数据源动态使用下列关键字。  
  
|关键字|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|字段的排序顺序的序列。<br /><br /> 这将设置为相同的选项**排序规则序列**中设置的对话框。|  
|COMPACT_DB|在数据库文件上执行数据压缩。 采用以下格式：COMPACT_DB = < path_name >< optionaL_sort_order >\<可选加密关键字 >。<br /><br /> 在使用 DSN 关键字在同一语句中使用 COMPACT_DB 关键字，此驱动程序将忽略 DSN 关键字。 因此，压缩的数据库并指定 DSN 是一个两步过程。|  
|CREATE_DB|创建一个数据库文件。 采用以下格式：CREATE_DB = < path_name >\<optional_sort 顺序 >< optional_ENCRYPT 关键字 >，其中的路径名称是 Microsoft Access 数据库的完整路径。 如果路径名称指定现有数据库，将返回错误。 排序顺序即可作为组运行时在 Microsoft 访问设置对话框中按创建按钮，显示新建数据库对话框中。 如果未不指定任何排序顺序，则使用常规。<br /><br /> 在使用 DSN 关键字在同一语句中使用 CREATE_DB 关键字，此驱动程序将忽略 DSN 关键字。 因此，创建数据库并指定 DSN 是一个两步过程。当使用 CREATE_DB 关键字，如果要创建的 Microsoft Access 数据库的路径名称中包含一个或多个空格，然后整个路径名引必须括在双引号引起来，如以下示例所示：<br /><br /> "C:\PROGRAM FILES\COMMON FILES\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb (no quotation marks needed)|  
|CREATE_SYSDB|创建一个系统数据库文件。 采用以下格式：CREATE_SYSDB =\<路径名称 >\<可选排序顺序 >，其中的路径名称是 Microsoft Access 数据库的完整路径。 如果路径名称指定现有数据库，将返回错误。 排序顺序就会为组启动中**新的数据库**对话框中显示时**创建**中单击按钮**ODBC Microsoft 访问设置**对话框。 如果未不指定任何排序顺序，则使用常规。|  
|CREATE_V2DB|创建与 Microsoft Access 2.0 兼容的数据库文件。 采用以下格式：CREATE_V2DB =\<路径名称 >\<可选排序顺序 >，其中的路径名称是 Microsoft Access 数据库的完整路径。 如果路径名称指定现有数据库，将返回错误。 排序顺序即可作为组运行时在 Microsoft 访问设置对话框中按创建按钮，显示新建数据库对话框中。 如果未不指定任何排序顺序，则使用常规。<br /><br /> 在使用 DSN 关键字在同一语句中使用 CREATE_V2DB 关键字，此驱动程序将忽略 DSN 关键字。 因此，创建数据库并指定 DSN 是一个两步过程。<br /><br /> 当使用 CREATE_V2DB 关键字，如果要创建的 Microsoft Access 数据库的路径名称中包含一个或多个空格，然后整个路径名引必须括在双引号引起来，如以下示例所示：<br /><br /> "C:\PROGRAM FILES\COMMON FILES\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb （不需要引号）|  
|DBQ|数据库文件的名称。<br /><br /> 这将设置为相同的选项**数据库**中设置的对话框。|  
|DEFAULTDIR|路径规范，以将数据库文件。|  
|DESCRIPTION|数据源中的数据说明。<br /><br /> 这将设置为相同的选项**说明**中设置的对话框。|  
|DRIVER|路径规范，以驱动程序 DLL。|  
|DRIVERID|驱动程序的一个整数 ID。  25 (Microsoft Access)|  
|FIL|文件类型的 Microsoft Access 的 MS Access|  
|IMPLICITCOMMITSYNC|确定 Microsoft Access 驱动程序是否将以异步方式执行内部或隐式提交。 此值最初设置为"是"，意味着 Microsoft Access 驱动程序将等待完成的内部/隐式事务中的提交。<br /><br /> 此选项的值不应更改而无需仔细考虑的后果。 有关选项的详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。<br /><br /> 这将设置为相同的选项**ImplicitCommitSync**中设置的对话框。|  
|MAXBUFFERSIZE|内部缓冲区，以千字节，Microsoft Access 用于传输数据到 \ 来自磁盘的大小。 默认缓冲区大小为 2048 KB （显示为 2048年）。 可以使用任何整除 256 的整数值。 这将设置为相同的选项**缓冲区大小**中设置的对话框。|  
|MAXSCANROWS|要设置基于现有数据的列的数据类型时进行扫描的行数。<br /><br /> 可以为要扫描的行输入一个介于 1 到 16。 默认值为 8;如果设置为 0，将扫描所有行。 （限制以外的数字将返回错误。）<br /><br /> 这将设置为相同的选项**扫描的行数**中设置的对话框。|  
|PAGETIMEOUT|以毫秒为单位，页 （如果不使用） 被删除前保留在缓冲区中指定时间的段。 默认值为 5 的十分之几秒的第二个 （0.5 秒为单位）。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这将设置为相同的选项**页超时**中设置的对话框。|  
|PWD|密码。|  
|READONLY|若要使文件只读的;如果为 FALSE，则若要使文件不是只读的。<br /><br /> 这将设置为相同的选项**Read Only**中设置的对话框。|  
|REPAIR_DB|修复损坏的提交过程中发生故障的数据库。<br /><br /> 在使用 DSN 关键字在同一语句中使用 REPAIR_DB 关键字，此驱动程序将忽略 DSN 关键字。 因此，修复数据库，并指定 DSN 是一个两步过程。|  
|SYSTEMDB|对于 Microsoft Access 驱动程序，系统数据库文件的路径规范。<br /><br /> 这将设置为相同的选项**系统数据库**中设置的对话框。|  
|线程|要使用的引擎的后台线程数。 此值默认为 3，但可以进行更改。<br /><br /> 这将设置为相同的选项**线程**中设置的对话框。|  
|UID|对于 Microsoft Access 驱动程序，用户 ID 名称将使用登录名。|  
|USERCOMMITSYNC|确定 Microsoft Access 驱动程序是否将以异步方式执行用户定义的事务。 此值最初设置为"是"，意味着 Microsoft Access 驱动程序将等待提交在用户定义事务中才能完成。<br /><br /> 此选项的值不应更改而无需仔细考虑的后果。 有关选项的详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。<br /><br /> 这将设置为相同的选项**UserCommitSync**中设置的对话框。|
