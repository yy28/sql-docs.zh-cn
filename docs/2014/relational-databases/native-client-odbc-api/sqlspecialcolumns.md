---
title: SQLSpecialColumns |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3a324381f44a19866ebdeba6dac1c319c0d10224
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026766"
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
  当请求行标识符 (*IdentifierType* SQL_BEST_ROWID)， **SQLSpecialColumns**任何请求之外 SQL_SCOPE_CURROW 范围，则返回空结果集 （没有任何数据行）。 生成的结果集指示仅在此作用域内这些列有效。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持标识符的伪列。 **SQLSpecialColumns**结果集将作为 SQL_PC_NOT_PSEUDO 标识的所有列。  
  
 **SQLSpecialColumns**可以执行对静态游标。 尝试执行**SQLSpecialColumns**上 SQL_SUCCESS_WITH_INFO，该值指示游标类型已更改可更新 （键集驱动或动态） 返回。  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>SQLSpecialColumns 对日期和时间增强功能的支持  
 有关值的信息的列 DATA_TYPE、 TYPE_NAME、 COLUMN_SIZE、 BUFFER_LENGTH 和 DECIMAL_DIGTS 为日期/时间类型返回，请参阅[目录元数据](../native-client-odbc-date-time/metadata-catalog.md)。  
  
 有关更多常规信息，请参阅[日期和时间改进&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>SQLSpecialColumns 对大型 CLR UDT 的支持  
 **SQLSpecialColumns**支持大型 CLR 用户定义类型 (Udt)。 有关详细信息，请参阅[Large CLR User-Defined 类型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLSpecialColumns 函数](http://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  