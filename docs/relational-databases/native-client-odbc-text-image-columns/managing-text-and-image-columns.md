---
title: 管理文本和图像列 |微软文档
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3ac58e59f66dd107a9523a42f5647c90b4fb737
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297707"
---
# <a name="managing-text-and-image-columns"></a>管理 Text 和 Image 列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**文本****、ntext**和**图像**数据（也称为长数据）是字符或二进制字符串数据类型，可以保存数据值太大，无法放入**字符****、varchar、****二进制**或**varbinary**列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**文本**数据类型映射到 ODBC SQL_LONGVARCHAR数据类型;**ntext**地图到SQL_WLONGVARCHAR;和**图像**映射到SQL_LONGVARBINARY。 某些数据项（例如很长的文档或大位图）可能因太大而无法在内存中合理存储。 若要从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]顺序零件中检索长数据，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序使应用程序能够调用[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)。 要按顺序部件发送长数据，应用程序可以调用[SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md)。 在执行时发送其数据的参数称为执行时数据参数。  
  
 应用程序实际上可以使用**SQLPutData**或**SQLGetData**编写或检索任何类型的数据（而不仅仅是长数据），尽管只能分批发送或检索**字符**和**二进制**数据。 但是，如果数据足够小，可以容纳单个缓冲区，则通常没有理由使用**SQLPutData**或**SQLGetData**。 将单一缓冲区绑定到参数或列更简单。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [绑定与未绑定的 Text 和 Image 列](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [有日志记录的修改与无日志记录的修改](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [执行时数据和 Text、ntext 或 Image 列](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (ODBC)](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
