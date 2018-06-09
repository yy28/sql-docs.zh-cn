---
title: 管理文本和图像列 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-text-image-columns
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 300caa16e74ee36e740c901a295c1c30c1723d33
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707235"
---
# <a name="managing-text-and-image-columns"></a>管理 Text 和 Image 列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **文本**， **ntext**，和**映像**数据 （也称为长整型数据） 是字符或二进制字符串数据类型，可以容纳数据值太大而无法放入**char**， **varchar**，**二进制**，或**varbinary**列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **文本**数据类型映射到 ODBC SQL_LONGVARCHAR 数据类型;**ntext**映射到 SQL_WLONGVARCHAR; 和**映像**映射到 SQL_LONGVARBINARY。 某些数据项（例如很长的文档或大位图）可能因太大而无法在内存中合理存储。 检索从的长整型数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中序列部分[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序可让应用程序调用[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)。 若要在序列部分发送的长整型数据，应用程序可以调用[SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md)。 在执行时发送其数据的参数称为执行时数据参数。  
  
 应用程序可以实际写入或检索任何类型的数据 （不持续一段时间数据） 与**SQLPutData**或**SQLGetData**，尽管唯一**字符**和**二进制**可发送或在部件中检索数据。 但是，如果数据不足够小，无法放在单个缓冲区，则通常无需使用**SQLPutData**或**SQLGetData**。 将单一缓冲区绑定到参数或列更简单。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [绑定与未绑定的 Text 和 Image 列](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [有日志记录的修改与无日志记录的修改](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [执行时数据和 Text、ntext 或 Image 列](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client (ODBC)](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
