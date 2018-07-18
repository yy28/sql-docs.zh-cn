---
title: 字符数据的自动转换 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], autotranslating character data
- data types [ODBC], autotranslating character data
- ACPs
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- AutoTranslate feature
- ANSI code pages
- character data autotranslation [ODBC]
- autotranslating character data
- SQL Server Native Client ODBC driver, data types
- ODBC data types, autotranslating character data
ms.assetid: 86a8adda-c5ad-477f-870f-cb370c39ee13
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7921d0bc0c41fc5053ceb0fbcd95e56dc4b4fd5a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409996"
---
# <a name="autotranslation-of-character-data"></a>字符数据的自动转换
  字符数据，例如 ANSI 字符 SQL_C_CHAR 用声明的变量或数据存储在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用**char**， **varchar**，或**文本**数据类型，可以表示只有有限的数量的字符。 对于每个字符使用一个字节进行存储的字符数据，它只能表示 256 个字符。 使用客户端计算机的 ANSI 代码页 (ACP) 解释存储在 SQL_C_CHAR 变量中的值。 使用存储的值**char**， **varchar**，或**文本**服务器上的数据类型使用服务器的 ACP 进行评估。  
  
 如果在服务器和客户端使用相同的 ACP，则它们不会出现问题在解释存储在 SQL_C_CHAR、 的值**char**， **varchar**，或**文本**对象。 如果服务器和客户端具有不同的 Acp，则可能会从客户端 SQL_C_CHAR 数据解释为在服务器上不同的字符，如果在使用**char**， **varchar**，或**文本**列、 变量或参数。 例如，包含值 0xA5 字符字节被解释为字符 Ñ 使用代码页 437 则在计算机上，运行代码页 1252年的计算机上解释为日元签名 （リ）。  
  
 Unicode 数据在存储时每个字符使用两个字节。 Unicode 规范涵盖所有扩展字符，因此每一 Unicode 字符都会在所有计算机上解释为相同的字符。  
  
 AutoTranslate 功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序将尝试最大程度减少具有不同的代码页中客户端和服务器之间移动字符数据的问题。 可以在的连接字符串中设置 AutoTranslate [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md)中的配置字符串[SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)，或配置适用于数据源时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC使用 ODBC 管理器的驱动程序。  
  
 如果 AutoTranslate 设置为"no"，客户端上的 SQL_C_CHAR 变量之间移动数据会进行任何转换并**char**， **varchar**，或**文本**列、 变量，中的参数或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 如果数据包含扩展字符并且客户端和服务器计算机使用不同的代码页，则位模式在这两台计算机上会得到不同的解释。 如果这两台计算机使用相同的代码页，则数据将得到相同的解释。  
  
 如果 AutoTranslate 设置为"yes"， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序使用 Unicode 转换在客户端上的 SQL_C_CHAR 变量之间移动数据和**char**， **varchar**，或**文本**列、 变量或参数中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库：  
  
-   当数据发送到客户端上的 SQL_C_CHAR 变量从**char**， **varchar**，或**文本**列、 变量或参数中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库，ODBC驱动程序首先转换为从 sql_c_char 转换使用的客户端，然后从 Unicode 字符使用服务器的 ACP 回 ACP Unicode。  
  
-   从发送数据**char**， **varchar**，或**文本**列、 变量或参数中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库添加到客户端上的SQL_C_CHAR变量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序首先转换为从字符 Unicode 使用的服务器，然后从 Unicode 回 SQL_C_CHAR 使用客户端的 ACP ACP。  
  
 因为所有这些转换由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序执行客户端，服务器 ACP 必须是一个客户端计算机上安装的代码页。  
  
 通过 Unicode 对字符进行转换可确保存在于两个代码页中的所有字符都能得到正确的转换。 但是，如果存在于其中一个代码页的某个字符在另一个代码页中不存在，则该字符在目标代码页中将无法表示。 例如，代码页 1252 包含注册商标符号 (®)，而代码页 437 则不包含此符号。  
  
 AutoTranslate 设置对以下转换没有任何影响：  
  
-   字符 SQL_C_CHAR 客户端变量和 Unicode 之间移动数据**nchar**， **nvarchar**，或**ntext**列、 变量或参数中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
-   Unicode SQL_C_WCHAR 客户端变量和字符之间移动数据**char**， **varchar**，或**文本**列、 变量或参数中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
 在数据从字符移动到 Unicode 时，始终必须对其进行转换。  
  
## <a name="see-also"></a>请参阅  
 [处理结果&#40;ODBC&#41;](processing-results-odbc.md)   
 [排序规则和 Unicode 支持](../collations/collation-and-unicode-support.md)  
  
  
