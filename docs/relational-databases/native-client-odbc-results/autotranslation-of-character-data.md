---
title: 字符数据的自动翻译 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a8672f748af8d643fa39038be030efa5d434dc8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297877"
---
# <a name="autotranslation-of-character-data"></a>字符数据的自动转换
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  字符数据（如用SQL_C_CHAR或存储在使用**字符****、varchar**或**文本**数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中存储的数据声明的 ANSI 字符变量）只能表示有限数量的字符。 对于每个字符使用一个字节进行存储的字符数据，它只能表示 256 个字符。 使用客户端计算机的 ANSI 代码页 (ACP) 解释存储在 SQL_C_CHAR 变量中的值。 使用**字符****、varchar**或**文本**数据类型存储在服务器上的值使用服务器的 ACP 进行评估。  
  
 如果服务器和客户端具有相同的 ACP，则它们在解释存储在SQL_C_CHAR、**字符****、varchar**或**文本**对象中的值时没有问题。 如果服务器和客户端具有不同的 ASP，则来自客户端SQL_C_CHAR数据可能会被解释为服务器上的不同字符，如果它用于**字符****、varchar**或**文本**列、变量或参数。 例如，包含值 0xA5 的字符字节在计算机上使用代码页 437 将解释为字符 +，并在运行代码页 1252 的计算机上解释为日元符号 （*）。  
  
 Unicode 数据在存储时每个字符使用两个字节。 Unicode 规范涵盖所有扩展字符，因此每一 Unicode 字符都会在所有计算机上解释为相同的字符。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序的 AutoTranslate 功能尝试将在客户端和具有不同代码页的服务器之间移动字符数据时的问题降至最低。 自动转换可以在[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)的连接字符串中设置 ，在[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)的配置字符串中，或者使用 ODBC[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]管理员为本机客户端 ODBC 驱动程序配置数据源时。  
  
 当 AutoTranslate 设置为"否"时，对客户端和**数据库中的字符****、varchar**或**文本**列、变量或参数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之间移动 SQL_C_CHAR的数据不执行转换。 如果数据包含扩展字符并且客户端和服务器计算机使用不同的代码页，则位模式在这两台计算机上会得到不同的解释。 如果这两台计算机使用相同的代码页，则数据将得到相同的解释。  
  
 当 AutoTranslate 设置为"是"时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序使用 Unicode 转换在客户端和**数据库中的字符****、varchar**或**文本**列、变量或参数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之间移动 SQL_C_CHAR的数据：  
  
-   当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据从客户端上的SQL_C_CHAR变量发送到数据库中的**字符****、varchar**或**文本**列、变量或参数时，ODBC 驱动程序首先使用客户端的 ACP 从SQL_C_CHAR转换为 Unicode，然后使用服务器的 ACP 将 Unicode 转换回字符。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]当数据从数据库中的**字符****、varchar**或**文本**列、变量或参数发送到客户端上的SQL_C_CHAR变量时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序首先使用服务器的 ACP 从字符转换为 Unicode，然后使用客户端的 ACP 从 Unicode 转换回SQL_C_CHAR。  
  
 由于所有这些转换都由在客户端上执行的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序完成，因此服务器 ACP 必须是客户端计算机上安装的代码页之一。  
  
 通过 Unicode 对字符进行转换可确保存在于两个代码页中的所有字符都能得到正确的转换。 但是，如果存在于其中一个代码页的某个字符在另一个代码页中不存在，则该字符在目标代码页中将无法表示。 例如，代码页 1252 包含注册商标符号 (®)，而代码页 437 则不包含此符号。  
  
 AutoTranslate 设置对以下转换没有任何影响：  
  
-   在字符SQL_C_CHAR客户端变量和 Unicode **nchar、nvarchar**或**数据库中的 ntext**列、变量或参数之间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移动数据。 **nvarchar**  
  
-   在 Unicode SQL_C_WCHAR客户端变量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和字符**字符****、varchar**或**数据库中的文本**列、变量或参数之间移动数据。  
  
 在数据从字符移动到 Unicode 时，始终必须对其进行转换。  
  
## <a name="see-also"></a>另请参阅  
 [处理结果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
