---
title: SQLSpecialColumns |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8bba924c4a2258362986544a676eb09c87a51328
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43093818"
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  请求行标识符 (*IdentifierType* SQL_BEST_ROWID)， **SQLSpecialColumns**返回空结果集 （没有任何数据行） 的任何请求的除 sql_scope_currow 之外的作用域。 生成的结果集指示仅在此作用域内这些列有效。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持标识符的伪列。 **SQLSpecialColumns**结果集将所有列都标识为 SQL_PC_NOT_PSEUDO。  
  
 **SQLSpecialColumns**可以对静态游标执行。 尝试执行**SQLSpecialColumns**上可更新 （由键集驱动或动态） 返回 sql_success_with_info 以指示游标类型已更改。  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>SQLSpecialColumns 对日期和时间增强功能的支持  
 有关值的信息的列 DATA_TYPE、 TYPE_NAME、 COLUMN_SIZE、 BUFFER_LENGTH 和 DECIMAL_DIGTS 为日期/时间类型返回，请参阅[目录元数据](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 有关更多常规信息，请参阅[日期和时间改进&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>SQLSpecialColumns 对大型 CLR UDT 的支持  
 **SQLSpecialColumns**支持大型 CLR 用户定义类型 (Udt)。 有关详细信息，请参阅[Large CLR User-Defined 类型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLSpecialColumns 函数](http://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
