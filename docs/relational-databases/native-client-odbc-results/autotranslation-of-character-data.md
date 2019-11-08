---
title: 字符数据的自动转换 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c08a0987e11f25c3f5b535d8d26526db5bb14a38
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779178"
---
# <a name="autotranslation-of-character-data"></a>字符数据的自动转换
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  字符数据（如使用 SQL_C_CHAR 或使用**CHAR**、 **varchar**或**text**数据类型存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的数据）声明的字符数据只能表示有限数量的字符。 对于每个字符使用一个字节进行存储的字符数据，它只能表示 256 个字符。 使用客户端计算机的 ANSI 代码页 (ACP) 解释存储在 SQL_C_CHAR 变量中的值。 使用服务器上的**char**、 **varchar**或**text**数据类型存储的值将使用服务器的 ACP 进行计算。  
  
 如果服务器和客户端具有相同的 ACP，则在解释 SQL_C_CHAR、 **CHAR**、 **varchar**或**text**对象中存储的值时，它们没有任何问题。 如果服务器和客户端具有不同的 Acp，则从客户端 SQL_C_CHAR 的数据可能会在服务器上解释为不同的字符（如果在**CHAR**、 **varchar**或**text**列、变量或参数中使用）。 例如，在使用代码页437的计算机上，包含值0xA5 的字符字节被解释为字符-，并在运行代码页1252的计算机上解释为日元符号（¥）。  
  
 Unicode 数据在存储时每个字符使用两个字节。 Unicode 规范涵盖所有扩展字符，因此每一 Unicode 字符都会在所有计算机上解释为相同的字符。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序的 AutoTranslate 功能尝试最大程度地减少在客户端和具有不同代码页的服务器之间移动字符数据时出现的问题。 可以在[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)的连接字符串中设置 AutoTranslate，或者在[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)的配置字符串中设置，或者使用 ODBC 管理器为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序配置数据源。  
  
 如果将 AutoTranslate 设置为 "no"，则不会对客户端上的 SQL_C_CHAR 变量和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的**CHAR**、 **varchar**或**text**列、变量或参数之间移动的数据进行转换。 如果数据包含扩展字符并且客户端和服务器计算机使用不同的代码页，则位模式在这两台计算机上会得到不同的解释。 如果这两台计算机使用相同的代码页，则数据将得到相同的解释。  
  
 当 AutoTranslate 设置为 "yes" 时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序将使用 Unicode 来转换客户端上 SQL_C_CHAR 变量之间移动的数据，并使用**CHAR**、 **varchar**或**text**列、变量或参数在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据  
  
-   将数据从客户端上的 SQL_C_CHAR 变量发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的**CHAR**、 **varchar**或**text**列、变量或参数时，ODBC 驱动程序将首先使用客户端的 ACP 从 SQL_C_CHAR 转换为 Unicode，然后使用服务器的 ACP 从 Unicode 返回到字符。  
  
-   如果将数据从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的**char**、 **varchar**或**text**列、变量或参数发送到客户端上的 SQL_C_CHAR 变量，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client ODBC 驱动程序将首先使用 ACP 将字符转换为 Unicode，然后使用客户端的 ACP 从 Unicode 返回到 SQL_C_CHAR。  
  
 由于所有这些转换都是通过在客户端上执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序来完成的，因此服务器 ACP 必须是客户端计算机上安装的代码页之一。  
  
 通过 Unicode 对字符进行转换可确保存在于两个代码页中的所有字符都能得到正确的转换。 但是，如果存在于其中一个代码页的某个字符在另一个代码页中不存在，则该字符在目标代码页中将无法表示。 例如，代码页 1252 包含注册商标符号 (®)，而代码页 437 则不包含此符号。  
  
 AutoTranslate 设置对以下转换没有任何影响：  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的字符 SQL_C_CHAR 客户端变量和 Unicode **nchar**、 **nvarchar**或**ntext**列、变量或参数之间移动数据。  
  
-   在 Unicode SQL_C_WCHAR 客户端变量与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的**char**、 **varchar**或**text**列、变量或参数之间移动数据。  
  
 在数据从字符移动到 Unicode 时，始终必须对其进行转换。  
  
## <a name="see-also"></a>另请参阅  
 [处理结果&#40;ODBC&#41; ](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
