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
ms.openlocfilehash: 69f2c98678739a8b7879e152e13546f2bf9b9cc1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046929"
---
# <a name="driver-specific-connection-information"></a>特定于驱动程序的连接信息
**SQLConnect**假定数据源名称、用户 ID 和密码足以连接到数据源，并且可以在系统上存储所有其他连接信息。 这种情况通常并非如此。 例如，驱动程序可能需要使用一个用户 ID 和密码登录到服务器，并使用不同的用户 ID 和密码登录到 DBMS。 由于**SQLConnect**接受单个用户 id 和密码，因此，如果要使用**SQLConnect** ，则必须与系统上的数据源信息一起存储其他用户 id 和密码。 这是潜在的安全漏洞，应避免使用，除非密码已加密。  
  
 **SQLDriverConnect**允许驱动程序在连接字符串的关键字/值对中定义任意数量的连接信息。 例如，假设驱动程序需要数据源名称、服务器的用户 ID 和密码，以及 DBMS 的用户 ID 和密码。 始终使用 XYZ 公司数据源的自定义程序可能会提示用户输入 Id 和密码，并生成以下要传递给**SQLDriverConnect**的关键字/值对集或*连接字符串*：  
  
> [!NOTE]  
>  如果要连接到支持 Windows 身份验证的数据源提供程序，应在连接`Trusted_Connection=yes`字符串中指定而不是用户 ID 和密码信息。  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN** （数据源名称）关键字将数据源命名为， **UID**和**PWD**关键字指定服务器的用户 Id 和密码， **UIDDBMS**和**PWDDBMS**关键字指定 DBMS 的用户 id 和密码。 请注意，最后一个分号是可选的。 **SQLDriverConnect**分析此字符串;使用 XYZ Corp 数据源名称从系统检索其他连接信息，如服务器地址;并使用指定的用户 Id 和密码登录到服务器和 DBMS。  
  
 **SQLDriverConnect**中的关键字/值对必须遵循某些语法规则。 关键字及其值不应包含 **[]{}（），;？= \*！ @** 个字符。 **DSN**关键字的值不能只包含空格，并且不能包含前导空格。 由于注册表语法的原因，关键字和数据源名称不能包含反斜杠\\（）字符。 关键字-值对中的等号前后不允许有空格。  
  
 可以在对**SQLDriverConnect**的调用中使用**FILEDSN**关键字来指定包含数据源信息的文件的名称（请参阅本部分后面的[使用文件数据源进行连接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)）。 **SAVEFILE**关键字可用于指定 .dsn 文件的名称，在该文件中，将保存通过调用**SQLDriverConnect**进行的成功连接的关键字值对。 有关文件数据源的详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。
