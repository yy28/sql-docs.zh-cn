---
title: CompareEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareEnum
helpviewer_keywords:
- CompareEnum enumeration [ADO]
ms.assetid: bc8f710d-0621-4673-8d8e-0361e44abed0
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db29f164e3329044f0d4ed12d2353e206bb87172
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="compareenum"></a>CompareEnum
指定由其书签的两条记录的相对位置。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adCompareEqual**|1|指示书签相等。|  
|**adCompareGreaterThan**|2|指示第一个书签后第二个。|  
|**adCompareLessThan**|0|指示第一个书签之前第二个。|  
|**adCompareNotComparable**|4|指示书签不能进行比较。|  
|**adCompareNotEqual**|3|该值指示书签不相等或者未排序。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.Compare.EQUAL|  
|AdoEnums.Compare.GREATERTHAN|  
|AdoEnums.Compare.LESSTHAN|  
|AdoEnums.Compare.NOTCOMPARABLE|  
|AdoEnums.Compare.NOTEQUAL|  
  
## <a name="applies-to"></a>适用范围  
 [CompareBookmarks 方法 (ADO)](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [CompareBookmarks 方法 (ADO)](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)
