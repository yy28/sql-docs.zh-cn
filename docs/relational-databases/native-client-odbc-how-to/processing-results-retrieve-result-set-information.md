---
title: 检索结果集信息 （ODBC） |微软文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f1c65841db0fdfd386891cfbd03bdee483ce25f6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300367"
---
# <a name="processing-results---retrieve-result-set-information"></a>处理结果 - 检索结果集信息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-get-information-about-a-result-set"></a>获取有关结果集的信息  
  
1.  调用[SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)获取结果集中的列数。  
  
2.  对于结果集中的每个列：  
  
    -   致电[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)获取有关结果列的信息。  
  
     Or  
  
    -   调用[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)获取有关结果列的特定描述符信息。  
  
## <a name="see-also"></a>另请参阅  
[&#40;ODBC&#41;的流程结果](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[确定结果集的特征&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
