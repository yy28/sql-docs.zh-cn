---
title: SQLSpecialColumns |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ea811151e9c81ed515b774f279297d236c608f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63188738"
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
  请求行标识符（*IdentifierType* SQL_BEST_ROWID）时， **SQLSpecialColumns**为除 SQL_SCOPE_CURROW 以外的任何请求的作用域返回空的结果集（无数据行）。 生成的结果集指示仅在此作用域内这些列有效。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持标识符的伪列。 **SQLSpecialColumns**结果集将所有列标识为 SQL_PC_NOT_PSEUDO。  
  
 可以对静态游标执行**SQLSpecialColumns** 。 尝试对可更新的（键集驱动或动态）执行**SQLSpecialColumns**将返回 SQL_SUCCESS_WITH_INFO 指示游标类型已更改。  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>SQLSpecialColumns 对日期和时间增强功能的支持  
 有关为日期/时间类型 DATA_TYPE、TYPE_NAME、COLUMN_SIZE、BUFFER_LENGTH 和 DECIMAL_DIGTS 返回的列的值的信息，请参阅[目录元数据](../native-client-odbc-date-time/metadata-catalog.md)。  
  
 有关更多常规信息，请参阅[ODBC&#41;&#40;日期和时间改进](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>SQLSpecialColumns 对大型 CLR UDT 的支持  
 **SQLSpecialColumns**支持大型 CLR 用户定义类型（udt）。 有关详细信息，请参阅[&#40;ODBC&#41;的大型 CLR 用户定义类型](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLSpecialColumns 函数](https://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
