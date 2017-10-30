---
title: "特定于驱动程序的连接信息 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9e1624febc9b53c654c1b01f5aafb601b97b3cbf
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="driver-specific-connection-information"></a>特定于驱动程序的连接信息
**SQLConnect**假定数据源名称、 用户 ID 和密码是不足以连接到数据源，并且，可以在系统上存储的所有其他连接信息。 这不经常这种情况。 例如，驱动程序可能需要一个用户 ID 和密码登录到服务器以及其他用户 ID 和密码登录到 DBMS。 因为**SQLConnect**接受单个用户 ID 和密码，这意味着，其他用户 ID 和密码必须存储在系统上的数据源信息如果**SQLConnect**要使用。 这是潜在的安全违规行为，除非密码经过加密应当避免。  
  
 **SQLDriverConnect**允许驱动程序在连接字符串的关键字 / 值对中定义任意数量的连接信息。 例如，假设驱动程序需要数据源名称、 用户 ID 和密码的服务器，以及用户 ID 和密码的 DBMS。 始终使用 XYZ Corp 数据源的自定义程序可能会提示用户 Id 和密码，并生成以下集的关键字 / 值对，或*连接字符串，*要传递给**SQLDriverConnect**:  
  
> [!NOTE]  
>  如果你要连接到的数据源提供程序支持 Windows 身份验证，你应指定`Trusted_Connection=yes`而不是连接字符串中的用户 ID 和密码信息。  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN** （数据源名称） 关键字名称数据源， **UID**和**PWD**关键字指定的用户 ID 和密码的服务器和**UIDDBMS**和**PWDDBMS**关键字为 DBMS 中指定的用户 ID 和密码。 请注意，最后的分号是可选的。 **SQLDriverConnect**分析此字符串; 使用 XYZ Corp 数据源名称从系统，例如服务器地址; 中检索的其他连接信息并登录到服务器和使用指定的用户 Id 和密码的 DBMS。  
  
 关键字 / 值对中**SQLDriverConnect**必须遵循某些语法规则。 关键字和它们的值不应包含**[] {} （)，;？\*= ！ @**字符。 值**DSN**关键字不能只包含空格，并且不包含前导空格。 由于注册表语法中，关键字和数据源名称不能包含反斜杠 (\\) 字符。 中的关键字 / 值对的等号两侧不允许有空格。  
  
 **FILEDSN**关键字可以在调用中使用**SQLDriverConnect**以指定包含数据源信息的文件的名称 (请参阅[连接使用的文件数据源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，本部分中更高版本)。 **SAVEFILE**关键字可用来指定在其中进行成功的连接的关键字 / 值对的.dsn 文件的名称通过调用**SQLDriverConnect**将保存。 有关文件数据源的详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。

