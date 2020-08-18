---
description: SQLConfigDataSource（Access 驱动程序）
title: SQLConfigDataSource (Access 驱动程序) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: deb777e0d1d4a4e3ea9a45968256ad23dbeb56ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411983"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 用于动态添加、修改或删除数据源的 **SQLConfigDataSource** 函数使用以下关键字。  
  
|关键字|描述|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|字段的排序顺序。<br /><br /> 这会在 "安装程序" 对话框中设置与 **排序顺序** 相同的选项。|  
|COMPACT_DB|对数据库文件执行数据压缩。 具有以下格式： COMPACT_DB =<path_name><optionaL_sort_order>\<optional ENCRYPT keyword> 。<br /><br /> 在同一语句中使用带有 DSN 关键字的 COMPACT_DB 关键字时，此驱动程序将忽略 DSN 关键字。 因此，压缩数据库和指定 DSN 的过程分为两个步骤。|  
|CREATE_DB|创建数据库文件。 具有以下格式： CREATE_DB =<path_name>\<optional_sort-order><optional_ENCRYPT 关键字>，其中，路径名称是 Microsoft Access 数据库的完整路径。 如果路径名称指定了现有数据库，则将返回错误。 当在 "Microsoft Access 设置" 对话框中按 "创建" 按钮时，将在 "新建数据库" 对话框中设置排序顺序。 如果未指定排序顺序，则使用 "常规"。<br /><br /> 在同一语句中使用带有 DSN 关键字的 CREATE_DB 关键字时，此驱动程序将忽略 DSN 关键字。 因此，创建数据库和指定 DSN 的过程分为两个步骤。使用 CREATE_DB 关键字时，如果要创建的 Microsoft Access 数据库的路径名包含一个或多个空格，则必须用双引号将整个路径名括起来，如以下示例中所示：<br /><br /> "C:\PROGRAM FILES\COMMON FILES \ MyAccess"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB = C:\TEMP\test.mdb (不需要引号) |  
|CREATE_SYSDB|创建系统数据库文件。 具有以下格式： CREATE_SYSDB = \<path-name> \<optional-sort-order> ，其中，路径名称是 Microsoft Access 数据库的完整路径。 如果路径名称指定了现有数据库，则将返回错误。 当在 " **ODBC Microsoft Access 安装**" 对话框中单击 "**创建**" 按钮时，将在显示的 "**新建数据库**" 对话框中设置排序顺序。 如果未指定排序顺序，则使用 "常规"。|  
|CREATE_V2DB|创建与 Microsoft Access 2.0 兼容的数据库文件。 具有以下格式： CREATE_V2DB = \<path-name> \<optional-sort-order> ，其中，路径名称是 Microsoft Access 数据库的完整路径。 如果路径名称指定了现有数据库，则将返回错误。 当在 "Microsoft Access 设置" 对话框中按 "创建" 按钮时，将在 "新建数据库" 对话框中设置排序顺序。 如果未指定排序顺序，则使用 "常规"。<br /><br /> 在同一语句中使用带有 DSN 关键字的 CREATE_V2DB 关键字时，此驱动程序将忽略 DSN 关键字。 因此，创建数据库和指定 DSN 的过程分为两个步骤。<br /><br /> 使用 CREATE_V2DB 关键字时，如果要创建的 Microsoft Access 数据库的路径名包含一个或多个空格，则必须用双引号将整个路径名括起来，如以下示例中所示：<br /><br /> "C:\PROGRAM FILES\COMMON FILES \ MyAccess"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB = C:\TEMP\test.mdb (不需要引号) |  
|DBQ|数据库文件的名称。<br /><br /> 这会在 "设置" 对话框中设置与 **数据库** 相同的选项。|  
|DEFAULTDIR|数据库文件的路径规范。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这会在 "设置" 对话框中设置与 " **描述** " 相同的选项。|  
|DRIVER|驱动程序 DLL 的路径规范。|  
|DRIVERID|驱动程序的整数 ID。  25 (Microsoft Access) |  
|FIL|Microsoft Access 的文件类型 MS 访问权限|  
|IMPLICITCOMMITSYNC|确定 Microsoft Access 驱动程序是否将异步执行内部或隐式提交。 此值最初设置为 "是"，这意味着 Microsoft Access 驱动程序将等待内部/隐性事务中的提交完成。<br /><br /> 如果不仔细考虑后果，则不应更改此选项的值。 有关选项的详细信息，请参阅 *Microsoft Jet 数据库引擎程序员指南*。<br /><br /> 这会在 "设置" 对话框中设置与 " **ImplicitCommitSync** " 相同的选项。|  
|MAXBUFFERSIZE|Microsoft Access 用于将数据传输到磁盘或从磁盘传输数据的内部缓冲区大小（kb）。 默认缓冲区大小为 2048 KB (显示为 2048) 。 可以使用任何可被256整除的整数值。 这会在 "设置" 对话框中设置与 **缓冲区大小** 相同的选项。|  
|MAXSCANROWS|基于现有数据设置列的数据类型时要扫描的行数。<br /><br /> 可以为要扫描的行输入一个介于1到16之间的数字。 该值默认为 8;如果设置为0，则扫描所有行。  (超出限制的数字将返回错误。 ) <br /><br /> 这会在 "安装程序" 对话框中设置与 **要扫描的行** 相同的选项。|  
|PAGETIMEOUT|如果未使用，则指定页 (的时间段（以毫秒为单位）) 在删除之前保留在缓冲区中。 默认值为每秒 (0.5 秒) 。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这会设置与 "设置" 对话框中 **页面超时** 相同的选项。|  
|PWD|密码。|  
|READONLY|若要使文件为只读，则为 TRUE;如果设置为 FALSE，则使文件不为只读。<br /><br /> 这会在 "设置" 对话框中设置与 " **只读** " 相同的选项。|  
|REPAIR_DB|修复在提交过程中发生的故障导致的数据库损坏。<br /><br /> 在同一语句中使用带有 DSN 关键字的 REPAIR_DB 关键字时，此驱动程序将忽略 DSN 关键字。 因此，修复数据库和指定 DSN 的过程分为两个步骤。|  
|SYSTEMDB|对于 Microsoft Access 驱动程序，则为系统数据库文件的路径规范。<br /><br /> 这会在 "设置" 对话框中设置与 " **系统数据库** " 相同的选项。|  
|线程|引擎要使用的后台线程数。 此值默认为3，但可以更改。<br /><br /> 这会设置与 "设置" 对话框中的 **线程** 相同的选项。|  
|UID|对于 Microsoft Access 驱动程序，为用于登录的用户 ID 名称。|  
|USERCOMMITSYNC|确定 Microsoft Access 驱动程序是否将以异步方式执行用户定义的事务。 此值最初设置为 "是"，这意味着 Microsoft Access 驱动程序将等待用户定义事务中的提交完成。<br /><br /> 如果不仔细考虑后果，则不应更改此选项的值。 有关选项的详细信息，请参阅 *Microsoft Jet 数据库引擎程序员指南*。<br /><br /> 这会在 "设置" 对话框中设置与 " **UserCommitSync** " 相同的选项。|
