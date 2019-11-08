---
title: 管理文本和图像列 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- data types [ODBC], mapping
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 7b543556-ff36-4d35-ac08-de96223d92cd
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 221d83188a3d48fe5383a109b878c7b5a59bdad5
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73758404"
---
# <a name="managing-text-and-image-columns"></a>管理 Text 和 Image 列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **text**、 **ntext**和**image**数据（也称为长数据）是字符或二进制字符串数据类型，这些数据类型可以保存数据值太大，无法放入**char**、 **varchar**、 **binary**或**varbinary**表列. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**文本**数据类型映射到 ODBC SQL_LONGVARCHAR 数据类型;**ntext**映射到 SQL_WLONGVARCHAR;和**图像**映射到 SQL_LONGVARBINARY。 某些数据项（例如很长的文档或大位图）可能因太大而无法在内存中合理存储。 若要从连续部分的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 检索长数据，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序允许应用程序调用[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)。 若要以连续部分发送长数据，应用程序可以调用[SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md)。 在执行时发送其数据的参数称为执行时数据参数。  
  
 应用程序实际上可以使用**SQLPutData**或**SQLGetData**来写入或检索任何类型的数据（而不只是长数据），尽管只能在部分中发送或检索**字符**和**二进制**数据。 但是，如果数据太小，足以容纳在单个缓冲区中，通常没有理由使用**SQLPutData**或**SQLGetData**。 将单一缓冲区绑定到参数或列更简单。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [绑定与未绑定的 Text 和 Image 列](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [记录的修改与无日志记录修改](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [执行时数据和 Text、ntext 或 Image 列](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (ODBC)](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
