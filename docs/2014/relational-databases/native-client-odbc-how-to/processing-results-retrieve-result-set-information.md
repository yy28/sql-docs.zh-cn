---
title: 检索结果集信息 (ODBC) |Microsoft 文档
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
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ae6d8f1c5640ee0dc8f63b54a2117057b8f334e2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025905"
---
# <a name="retrieve-result-set-information-odbc"></a>检索结果集信息 (ODBC)
    
### <a name="to-get-information-about-a-result-set"></a>获取有关结果集的信息  
  
1.  调用[SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md)以获取结果集中的列数。  
  
2.  对于结果集中的每个列：  
  
    -   调用[SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md)以获取有关结果列的信息。  
  
     或  
  
    -   调用[SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md)若要获取特定的描述符信息结果列。  
  
## <a name="see-also"></a>请参阅  
 [处理结果操作指南主题&#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)   
 [确定结果集的特征&#40;ODBC&#41;](../native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  