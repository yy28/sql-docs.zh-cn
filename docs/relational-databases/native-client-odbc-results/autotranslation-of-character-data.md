---
title: 字符数据 Autotranslation |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-results
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
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
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c7306a8aff3dc8e0e85927dee7fd3a7afbae96fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="autotranslation-of-character-data"></a>字符数据的自动转换
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  字符数据，如 ANSI 字符用 SQL_C_CHAR 声明的变量或数据存储在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用**char**， **varchar**，或**文本**数据类型，可以表示仅有限的数量的字符。 对于每个字符使用一个字节进行存储的字符数据，它只能表示 256 个字符。 使用客户端计算机的 ANSI 代码页 (ACP) 解释存储在 SQL_C_CHAR 变量中的值。 使用存储的值**char**， **varchar**，或**文本**使用服务器的 ACP 评估的服务器上的数据类型。  
  
 如果服务器和客户端都有相同的 ACP，则它们不具有在解释 SQL_C_CHAR 中, 存储的值的任何问题**char**， **varchar**，或**文本**对象。 如果服务器和客户端具有不同 ACPs，则可能被从客户端的 SQL_C_CHAR 数据解释为服务器上不同的字符，如果它在中使用**char**， **varchar**，或**文本**列、 变量或参数。 例如，包含值 0xA5 字符字节解释为字符 Ñ 使用代码页 437 的计算机上，并可以解释为日元登录 （¥） 运行代码页 1252年的计算机上。  
  
 Unicode 数据在存储时每个字符使用两个字节。 Unicode 规范涵盖所有扩展字符，因此每一 Unicode 字符都会在所有计算机上解释为相同的字符。  
  
 AutoTranslate 功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序尝试尽量减少客户端和服务器之间移动字符数据中具有不同的代码页的问题。 可以在的连接字符串中设置 AutoTranslate [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)中的配置字符串[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)，或配置数据源时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC使用 ODBC 管理器的驱动程序。  
  
 当 AutoTranslate 设置为"no"时，任何转换都将在客户端上的 SQL_C_CHAR 变量之间移动数据和**char**， **varchar**，或**文本**列、 变量中的参数或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 如果数据包含扩展字符并且客户端和服务器计算机使用不同的代码页，则位模式在这两台计算机上会得到不同的解释。 如果这两台计算机使用相同的代码页，则数据将得到相同的解释。  
  
 当 AutoTranslate 设置为"yes"， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序使用 Unicode 转换客户端上的 SQL_C_CHAR 变量之间移动数据和**char**， **varchar**，或**文本**列、 变量或参数中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库：  
  
-   当数据发送到客户端上的 SQL_C_CHAR 变量从**char**， **varchar**，或**文本**列、 变量或参数中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库，ODBC驱动程序首先从 SQL_C_CHAR 转换，为使用的客户端，然后从 Unicode 字符使用服务器的 ACP 回 ACP 的 Unicode。  
  
-   从发送数据**char**， **varchar**，或**文本**列、 变量或参数中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上客户端， SQL_C_CHAR变量的数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序首先从字符转换，为使用的服务器，然后从 Unicode 回 SQL_C_CHAR 使用的客户端 ACP ACP 的 Unicode。  
  
 因为所有这些转换由执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序执行客户端服务器 ACP 上必须是安装在客户端计算机上的代码页。  
  
 通过 Unicode 对字符进行转换可确保存在于两个代码页中的所有字符都能得到正确的转换。 但是，如果存在于其中一个代码页的某个字符在另一个代码页中不存在，则该字符在目标代码页中将无法表示。 例如，代码页 1252 包含注册商标符号 (®)，而代码页 437 则不包含此符号。  
  
 AutoTranslate 设置对以下转换没有任何影响：  
  
-   字符 SQL_C_CHAR 客户端变量和 Unicode 之间移动数据**nchar**， **nvarchar**，或**ntext**列、 变量或参数中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
-   Unicode SQL_C_WCHAR 客户端变量和字符之间移动数据**char**， **varchar**，或**文本**列、 变量或参数中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
 在数据从字符移动到 Unicode 时，始终必须对其进行转换。  
  
## <a name="see-also"></a>另请参阅  
 [处理结果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
