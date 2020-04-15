---
title: SQL 配置数据源（访问驱动程序） |微软文档
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
ms.openlocfilehash: 48668525b578845fc330881d7c7de503d69d0928
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284047"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLConfigDataSource**函数用于动态添加、修改或删除数据源，使用以下关键字。  
  
|关键字|描述|  
|-------------|-----------------|  
|整理顺序|字段排序的顺序。<br /><br /> 这将设置与设置对话框中 **"整理序列"** 相同的选项。|  
|COMPACT_DB|对数据库文件执行数据压缩。 具有以下格式：COMPACT_DB*<path_name><optionaL_sort_order>\<可选的 ENCRYPT 关键字>。<br /><br /> 当将 COMPACT_DB 关键字使用相同的语句与 DSN 关键字时，此驱动程序将忽略 DSN 关键字。 因此，压缩数据库和指定 DSN 是一个两步过程。|  
|CREATE_DB|创建数据库文件。 具有以下格式：CREATE_DB* \<<>optional_sort顺序><optional_ENCRYPT关键字>>path_name，其中路径名称是 Microsoft Access 数据库的完整路径。 如果路径名称指定现有数据库，则将返回错误。 排序顺序将与在 Microsoft 访问设置对话框中按下"创建"按钮时显示的"新建数据库"对话框中设置。 如果未指定排序顺序，则使用"常规"。<br /><br /> 当将CREATE_DB关键字使用相同的语句与 DSN 关键字时，此驱动程序将忽略 DSN 关键字。 因此，创建数据库并指定 DSN 是一个两步过程。使用 CREATE_DB 关键字时，如果要创建的 Microsoft Access 数据库的路径名称包含一个或多个空格，则整个路径名称必须用双引号括起来，如以下示例所示：<br /><br /> "C：程序文件_共享文件]MyAccess.mdb"<br /><br /> "C：_程序文件\访问2.mdb"<br /><br /> CREATE_DB_C：\TEMP_test.mdb（无需引号）|  
|CREATE_SYSDB|创建系统数据库文件。 具有以下格式：CREATE_SYSDB=\<路径名称>\<可选排序顺序>，其中路径名称是 Microsoft Access 数据库的完整路径。 如果路径名称指定现有数据库，则将返回错误。 排序顺序将如在**ODBC 微软访问设置**对话框中单击 **"创建**"按钮时显示的"**新建数据库**"对话框中设置。 如果未指定排序顺序，则使用"常规"。|  
|CREATE_V2DB|创建与 Microsoft Access 2.0 兼容的数据库文件。 具有以下格式：CREATE_V2DB=\<路径名称>\<可选排序顺序>，其中路径名称是 Microsoft Access 数据库的完整路径。 如果路径名称指定现有数据库，则将返回错误。 排序顺序将与在 Microsoft 访问设置对话框中按下"创建"按钮时显示的"新建数据库"对话框中设置。 如果未指定排序顺序，则使用"常规"。<br /><br /> 当将CREATE_V2DB关键字使用相同的语句与 DSN 关键字时，此驱动程序将忽略 DSN 关键字。 因此，创建数据库并指定 DSN 是一个两步过程。<br /><br /> 使用CREATE_V2DB关键字时，如果要创建的 Microsoft Access 数据库的路径名称包含一个或多个空格，则整个路径名称必须用双引号括起来，如以下示例所示：<br /><br /> "C：程序文件_共享文件]MyAccess.mdb"<br /><br /> "C：_程序文件\访问2.mdb"<br /><br /> CREATE_V2DB_C：\TEMP_test.mdb（无需引号）|  
|DBQ|数据库文件的名称。<br /><br /> 这将在设置对话框中设置与**数据库**相同的选项。|  
|默认DIR|数据库文件的路径规范。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这将设置与设置对话框中的 **"说明"** 相同的选项。|  
|DRIVER|驱动程序 DLL 的路径规范。|  
|驱动程序 ID|驱动程序的整数 ID。  25 （微软访问）|  
|FIL|文件类型 MS 访问微软访问|  
|隐式提交同步|确定 Microsoft Access 驱动程序将异步执行内部或隐式提交。 此值最初设置为"是"，这意味着 Microsoft Access 驱动程序将等待内部/隐式事务中的提交完成。<br /><br /> 如果不仔细考虑后果，不应改变这一备选办法的价值。 有关该选项的详细信息，请参阅 Microsoft*喷气数据库引擎程序员指南*。<br /><br /> 这将在设置对话框中设置与 **"隐式提交同步"** 相同的选项。|  
|最大缓冲大小|Microsoft Access 用于将数据传输到磁盘和从磁盘传输的内部缓冲区（以千字节为单位）的大小。 默认缓冲区大小为 2048 KB（显示为 2048）。 可以使用任何被 256 整数整数值可分割。 这将在设置对话框中设置与**缓冲区大小**相同的选项。|  
|马克斯坎罗斯|根据现有数据设置列的数据类型时要扫描的行数。<br /><br /> 可以输入从 1 到 16 的数字来扫描行。 该值默认为 8;如果设置为 0，则扫描所有行。 （超出限制的数字将返回错误。<br /><br /> 这将在设置对话框中设置与 **"要扫描的行"** 相同的选项。|  
|页面超时|指定页面（如果不使用）在删除之前保留在缓冲区中的时间段（以毫秒为单位）。 默认值为五十分之一秒（0.5 秒）。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这将在设置对话框中设置与**页面超时**相同的选项。|  
|PWD|密码。|  
|READONLY|TRUE 使文件为只读;FALSE 使文件不只读。<br /><br /> 这将在设置对话框中设置与 **"只读"** 相同的选项。|  
|REPAIR_DB|修复因提交过程中发生的故障而损坏的数据库。<br /><br /> 当将 REPAIR_DB 关键字使用相同的关键字与 DSN 关键字一起使用时，此驱动程序将忽略 DSN 关键字。 因此，修复数据库和指定 DSN 是一个两步过程。|  
|系统DB|对于 Microsoft Access 驱动程序，系统数据库文件的路径规范。<br /><br /> 这将在设置对话框中设置与**系统数据库**相同的选项。|  
|线程|发动机要使用的后台线程数。 此值默认为 3，但可以更改。<br /><br /> 这将设置与设置对话框中的 **"线程"** 相同的选项。|  
|UID|对于 Microsoft Access 驱动程序，用于登录的用户 ID 名称。|  
|用户提交同步|确定 Microsoft Access 驱动程序是否会异步执行用户定义的事务。 此值最初设置为"是"，这意味着 Microsoft Access 驱动程序将等待用户定义的事务中的提交完成。<br /><br /> 如果不仔细考虑后果，不应改变这一备选办法的价值。 有关该选项的详细信息，请参阅 Microsoft*喷气数据库引擎程序员指南*。<br /><br /> 这将在设置对话框中设置与**用户提交同步**相同的选项。|
