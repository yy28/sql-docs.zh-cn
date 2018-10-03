---
title: 特定于驱动程序的连接信息 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3852e713e517828e83e74bf7fb291ef20865532
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47797218"
---
# <a name="driver-specific-connection-information"></a>特定于驱动程序的连接信息
**SQLConnect**假定数据源名称、 用户 ID 和密码足以连接到数据源并且，可以在系统上存储的所有其他连接信息。 这经常是不这种情况。 例如，驱动程序可能需要一个用户 ID 和密码登录到服务器的另一个用户 ID 和密码登录到 DBMS。 因为**SQLConnect**接受单个用户 ID 和密码，这意味着，用户 ID 和密码必须存储在系统上的数据源信息如果**SQLConnect**时要使用。 这是可能出现安全违规，除非密码进行加密，否则应避免使用。  
  
 **SQLDriverConnect**允许驱动程序在连接字符串关键字 / 值对中定义任意数量的连接信息。 例如，假设驱动程序需要数据源名称、 用户 ID 和密码的服务器，以及用户 ID 和密码为 DBMS。 始终使用 XYZ Corp 数据源的自定义程序可能会提示用户输入 Id 和密码并生成以下一组关键字 / 值对，或*连接字符串*要传递给**SQLDriverConnect**:  
  
> [!NOTE]  
>  如果您要连接到的数据源提供程序支持 Windows 身份验证，则应指定`Trusted_Connection=yes`而不是在连接字符串中的用户 ID 和密码信息。  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN** （数据源名称） 关键字名称数据源**UID**并**PWD**关键字指定的用户 ID 和密码的服务器和**UIDDBMS**并**PWDDBMS**关键字为 DBMS 指定用户 ID 和密码。 请注意，最后一个分号是可选的。 **SQLDriverConnect**分析此字符串; 使用 XYZ Corp 数据源名称的其他连接信息检索系统，例如服务器的地址; 并登录到服务器和数据库管理系统使用指定的用户 Id 和密码。  
  
 中的关键字值对**SQLDriverConnect**必须遵循某些语法规则。 关键字和它们的值不应包含 **[]{}（)，;？\*= ！ @** 字符。 值**DSN**关键字不能只包含空格，且不应包含前导空格。 由于注册表语法，关键字和数据源名称不能包含反斜杠 (\\) 字符。 关键字值对中的等号两侧不允许有空格。  
  
 **FILEDSN**可以对的调用中使用关键字**SQLDriverConnect**若要指定包含数据源信息的文件的名称 (请参阅[连接使用的文件数据源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)稍后在本部分中)。 **SAVEFILE**关键字可用于指定在其中进行成功连接的关键字 / 值对的.dsn 文件的名称通过调用**SQLDriverConnect**将保存。 有关文件的数据源的详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。
