---
title: "PageSize 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset15::PageSize
helpviewer_keywords: PageSize property [ADO]
ms.assetid: e57930a6-46c4-4a17-a3b6-f79e94d5c9c7
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9c0417012a1c68d0a3e3951a11f3a9ec84d8e89e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="pagesize-property-ado"></a>PageSize 属性 (ADO)
指示构成多少条记录中的一个页[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**值，该值指示在页面上的记录数。 默认值是**10**。  
  
## <a name="remarks"></a>注释  
 使用**PageSize**属性来确定多少条记录组成的数据的逻辑页。 建立的页大小，可使用[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)属性可以移到特定页的第一个记录。 当你想要允许用户逐页浏览数据，一次查看一定数量的记录时，这是 Web 服务器方案中十分有用。  
  
 可以在任何时候，设置此属性，其值将用于计算的特定页的第一个记录的位置。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [AbsolutePage、 PageCount，以及 PageSize 属性示例 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、 PageCount 和 PageSize 属性示例 （VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 属性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageCount 属性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
