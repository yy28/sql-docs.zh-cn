---
title: 特定于驱动程序的连接信息 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16c8c5fc4fd3ac63aa3613b41e530446dffec118
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305785"
---
# <a name="driver-specific-connection-information"></a>特定于驱动程序的连接信息
**SQLConnect**假定数据源名称、用户 ID 和密码足以连接到数据源，并且所有其他连接信息可以存储在系统上。 情况通常并非如此。 例如，驱动程序可能需要一个用户 ID 和密码才能登录到服务器，需要不同的用户 ID 和密码才能登录到 DBMS。 由于**SQLConnect**接受单个用户 ID 和密码，这意味着如果要使用**SQLConnect，** 则必须将其他用户 ID 和密码与系统上的数据源信息一起存储。 这是潜在的安全漏洞，除非密码被加密，否则应避免这样做。  
  
 **SQLDriverConnect**允许驱动程序在连接字符串的关键字值对中定义任意数量的连接信息。 例如，假设驱动程序需要数据源名称、服务器的用户 ID 和密码以及 DBMS 的用户 ID 和密码。 始终使用 XYZ Corp 数据源的自定义程序可能会提示用户输入 ID 和密码，并构建以下一组关键字-值对或*连接字符串，* 以传递给**SQLDriverConnect**：  
  
> [!NOTE]  
>  如果要连接到支持 Windows 身份验证的数据源提供程序，则应在连接字符串中指定`Trusted_Connection=yes`而不是用户 ID 和密码信息。  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN（** 数据源名称）关键字为数据源命名 **，UID**和**PWD**关键字指定服务器的用户 ID 和密码 **，UIDDBMS**和**PWDDBMS**关键字指定 DBMS 的用户 ID 和密码。 请注意，最终分号是可选的。 **SQLDriverConnect**解析此字符串;使用 XYZ Corp 数据源名称从系统检索其他连接信息，例如服务器地址;并使用指定的用户密码登录到服务器和 DBMS。  
  
 **SQLDriverConnect**中的关键字值对必须遵循某些语法规则。 关键字及其值不应包含**{}*（""""""""""""""""""""""""""""""""""""""""\*[！]** 字符。 **DSN**关键字的值不能仅包含空白，并且不应包含前导空格。 由于注册表语法，关键字和数据源名称不能包含反斜杠 （\\） 字符。 关键字值对中的等号周围不允许空格。  
  
 在调用**SQLDriverConnect**时，可以使用**FILESN**关键字指定包含数据源信息的文件的名称（请参阅本节后面的["使用文件数据源进行连接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)）。 **SAVEFILE**关键字可用于指定 .dsn 文件的名称，其中将保存调用**SQLDriverConnect**成功连接的关键字-值对。 有关文件数据源的详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。
