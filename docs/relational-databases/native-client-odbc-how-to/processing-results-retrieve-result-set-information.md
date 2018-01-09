---
title: "检索结果集信息 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d02d5d45b4b06a5c8e3e0ce016a6c5930d3c00fb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="processing-results---retrieve-result-set-information"></a>处理结果-检索结果集信息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-get-information-about-a-result-set"></a>获取有关结果集的信息  
  
1.  调用[SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)以获取结果集中的列数。  
  
2.  对于结果集中的每个列：  
  
    -   调用[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)以获取有关结果列的信息。  
  
     或  
  
    -   调用[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)若要获取特定的描述符信息结果列。  
  
## <a name="see-also"></a>另请参阅  
[处理结果 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[确定的特征的结果集 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
