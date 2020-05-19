---
title: 检索结果集信息（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3017f74b12eb18624f8a34e8a1289da18b70c93a
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82712698"
---
# <a name="retrieve-result-set-information-odbc"></a>检索结果集信息 (ODBC)
    
### <a name="to-get-information-about-a-result-set"></a>获取有关结果集的信息  
  
1.  调用[SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md)可获取结果集中的列数。  
  
2.  对于结果集中的每个列：  
  
    -   调用[SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md)以获取有关结果列的信息。  
  
     或  
  
    -   调用[SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md)可获取有关结果列的特定描述符信息。  
  
## <a name="see-also"></a>另请参阅  
 [处理结果操作指南主题 &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)   
 [确定结果集的特征 &#40;ODBC&#41;](../native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
