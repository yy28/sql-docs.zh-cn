---
title: 管理文本和图像列 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1316f093ac0d1f79c5155ae1be88df98f091bd8f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129456"
---
# <a name="managing-text-and-image-columns"></a>管理 Text 和 Image 列
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **文本**， **ntext**，和**映像**数据 （也称为长整型数据） 是字符或二进制字符串数据类型，可以容纳数据值太大而无法放入**char**， **varchar**，**二进制**，或**varbinary**列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **文本**数据类型映射到 ODBC SQL_LONGVARCHAR 数据类型;**ntext**映射到 SQL_WLONGVARCHAR; 和**映像**映射到 SQL_LONGVARBINARY。 某些数据项（例如很长的文档或大位图）可能因太大而无法在内存中合理存储。 检索从的长整型数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中序列部分[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序可让应用程序调用[SQLGetData](../native-client-odbc-api/sqlgetdata.md)。 若要在序列部分发送的长整型数据，应用程序可以调用[SQLPutData](../native-client-odbc-api/sqlputdata.md)。 在执行时发送其数据的参数称为执行时数据参数。  
  
 应用程序可以实际写入或检索任何类型的数据 （不持续一段时间数据） 与**SQLPutData**或**SQLGetData**，尽管唯一**字符**和**二进制**可发送或在部件中检索数据。 但是，如果数据不足够小，无法放在单个缓冲区，则通常无需使用**SQLPutData**或**SQLGetData**。 将单一缓冲区绑定到参数或列更简单。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [绑定与未绑定的 Text 和 Image 列](bound-vs-unbound-text-and-image-columns.md)  
  
-   [有日志记录的修改与无日志记录的修改](logged-vs-unlogged-modifications.md)  
  
-   [执行时数据和 Text、ntext 或 Image 列](data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client (ODBC)](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  