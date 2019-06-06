---
title: PageSize 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageSize
helpviewer_keywords:
- PageSize property [ADO]
ms.assetid: e57930a6-46c4-4a17-a3b6-f79e94d5c9c7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 28e08e6a62eaa631e5a1e476207b47e39cf75032
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706944"
---
# <a name="pagesize-property-ado"></a>PageSize 属性 (ADO)
指示构成多少条记录中的一页[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**值，该值指示在页面有多少条记录。 默认值是**10**。  
  
## <a name="remarks"></a>备注  
 使用**PageSize**属性来确定多少条记录组成的数据的逻辑页。 建立页面大小，可使用[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)属性将移动到特定页面的第一个记录。 当你想要允许用户逐页浏览数据，一次查看特定数量的记录时，这是在 Web 服务器方案中有用。  
  
 可以在任何时候，设置此属性，其值将用于计算某一特定页的第一个记录的位置。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [AbsolutePage、 PageCount、 和 PageSize 属性示例 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、 PageCount、 和 PageSize 属性示例 （VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 属性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageCount 属性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
