---
title: "SQLConfigDataSource （Access 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 27658fe72c79409a32435971bfac8d10ce92cded
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource （Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函数，用于添加、 修改或删除数据源动态使用下列关键字。  
  
|关键字|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|字段的排序顺序的序列。<br /><br /> 这将设置为相同的选项**排序规则序列**在安装程序对话框中。|  
|COMPACT_DB|在数据库文件上执行数据压缩。 采用以下格式： COMPACT_DB = < path_name >< optionaL_sort_order >\<可选加密关键字 >。<br /><br /> 在使用一个 DSN 关键字在同一语句中使用 COMPACT_DB 关键字，该驱动程序会忽略 DSN 关键字。 因此，压缩的数据库并指定 DSN 是一个两步过程。|  
|CREATE_DB|创建数据库文件。 采用以下格式： CREATE_DB = < path_name >\<optional_sort 顺序 >< optional_ENCRYPT 关键字 >，其中的路径名称是 Microsoft Access 数据库的完整路径。 如果路径名称指定的现有数据库，则将返回错误。 排序顺序将为组注册时在 Microsoft 访问设置对话框中按创建按钮，显示新数据库对话框中。 如果不指定任何排序顺序，则使用常规。<br /><br /> 在使用一个 DSN 关键字在同一语句中使用 CREATE_DB 关键字，该驱动程序会忽略 DSN 关键字。 因此，创建数据库并指定 DSN 是一个两步过程。当使用 CREATE_DB 关键字，如果要创建的 Microsoft Access 数据库的路径名包含一个或多个空格，然后整个路径名必须括在双引号括起来，如下面的示例中所示：<br /><br /> "C:\PROGRAM FILES\COMMON FILES\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb （不需要引号）|  
|CREATE_SYSDB|创建系统数据库文件。 采用以下格式： CREATE_SYSDB =\<路径名称 >\<可选排序顺序 >，其中的路径名称是 Microsoft Access 数据库的完整路径。 如果路径名称指定的现有数据库，则将返回错误。 排序顺序将设置为向上更改在**新数据库**对话框中显示时**创建**在单击按钮**ODBC Microsoft Access 安装**对话框。 如果不指定任何排序顺序，则使用常规。|  
|CREATE_V2DB|创建与 Microsoft Access 2.0 兼容的数据库文件。 采用以下格式： CREATE_V2DB =\<路径名称 >\<可选排序顺序 >，其中的路径名称是 Microsoft Access 数据库的完整路径。 如果路径名称指定的现有数据库，则将返回错误。 排序顺序将为组注册时在 Microsoft 访问设置对话框中按创建按钮，显示新数据库对话框中。 如果不指定任何排序顺序，则使用常规。<br /><br /> 在使用一个 DSN 关键字在同一语句中使用 CREATE_V2DB 关键字，该驱动程序会忽略 DSN 关键字。 因此，创建数据库并指定 DSN 是一个两步过程。<br /><br /> 当使用 CREATE_V2DB 关键字，如果要创建的 Microsoft Access 数据库的路径名包含一个或多个空格，然后整个路径名必须括在双引号括起来，如下面的示例中所示：<br /><br /> "C:\PROGRAM FILES\COMMON FILES\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb （不需要引号）|  
|DBQ|数据库文件的名称。<br /><br /> 这将设置为相同的选项**数据库**在安装程序对话框中。|  
|DEFAULTDIR|所指定的路径的数据库文件。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这将设置为相同的选项**说明**在安装程序对话框中。|  
|DRIVER|到驱动程序 DLL 路径规范。|  
|DRIVERID|驱动程序的整数 ID。  25 (Microsoft Access)|  
|FIL|文件类型 MS Microsoft access 的访问|  
|IMPLICITCOMMITSYNC|确定 Microsoft Access 驱动程序是否将以异步方式执行内部或隐式提交。 此值最初设置为"是"，这意味着，Microsoft Access 驱动程序将等待完成的内部/隐式事务中的提交。<br /><br /> 此选项的值不应更改而无需仔细考虑后果。 有关选项的详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。<br /><br /> 这将设置为相同的选项**ImplicitCommitSync**在安装程序对话框中。|  
|MAXBUFFERSIZE|内部缓冲区大小，以千字节为单位，Microsoft Access 用于传输数据与其他磁盘。 默认缓冲区大小为 2048 KB （显示为 2048年）。 可以使用任何被 256 整除的整数值。 这将设置为相同的选项**缓冲区大小**在安装程序对话框中。|  
|MAXSCANROWS|要设置基于现有数据的列的数据类型时扫描的行数。<br /><br /> 可以为要扫描的行输入一个介于 1 到 16。 默认值为 8;如果设置为 0，将扫描所有行。 （限制以外的数字将返回错误。）<br /><br /> 这将设置为相同的选项**扫描的行数**在安装程序对话框中。|  
|PAGETIMEOUT|指定的时间段，以毫秒为单位，页 （如果未使用） 在被删除之前保留在缓冲区中。 默认值为 5 的十分之几秒 （0.5 秒为单位）。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这将设置为相同的选项**页超时**在安装程序对话框中。|  
|PWD|密码。|  
|READONLY|若要使文件成为只读的;如果为 FALSE，以使文件不是只读的。<br /><br /> 这将设置为相同的选项**Read Only**在安装程序对话框中。|  
|REPAIR_DB|修复损坏的提交过程中发生故障的数据库。<br /><br /> 在使用一个 DSN 关键字在同一语句中使用 REPAIR_DB 关键字，该驱动程序会忽略 DSN 关键字。 因此，修复数据库，并指定 DSN 是一个两步过程。|  
|SYSTEMDB|对于 Microsoft Access 驱动程序，系统数据库文件的路径规范。<br /><br /> 这将设置为相同的选项**系统数据库**在安装程序对话框中。|  
|线程|要使用的引擎的后台线程数。 此值默认为 3，但可以进行更改。<br /><br /> 这将设置为相同的选项**线程**在安装程序对话框中。|  
|UID|对于 Microsoft Access 驱动程序，用户 ID 名称使用登录名。|  
|USERCOMMITSYNC|确定 Microsoft Access 驱动程序是否将以异步方式执行用户定义的事务。 此值最初设置为"是"，这意味着，Microsoft Access 驱动程序将等待中用户定义的事务，若要完成的提交。<br /><br /> 此选项的值不应更改而无需仔细考虑后果。 有关选项的详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。<br /><br /> 这将设置为相同的选项**UserCommitSync**在安装程序对话框中。|
