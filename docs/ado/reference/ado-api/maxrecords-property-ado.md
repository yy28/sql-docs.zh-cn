---
title: MaxRecords 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MaxRecords
helpviewer_keywords:
- MaxRecords property [ADO]
ms.assetid: 20c76571-8c9a-482c-a99e-726ab1d93f8b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 130a67f10e8b7deaf8f48e94f949b43682f61ca1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707627"
---
# <a name="maxrecords-property-ado"></a>MaxRecords 属性 (ADO)
指示要返回到的记录的最大数[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从查询。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**值，该值指示要返回的记录的最大数。 默认值为零 (**0**)，这意味着没有限制。  
  
## <a name="remarks"></a>备注  
 使用**MaxRecords**属性来限制从数据源的提供程序返回的记录数。 此属性的默认设置为零，这意味着访问接口将返回所有请求的记录。  
  
 **MaxRecords**属性为读/写时**记录集**打开时为已关闭，只读的。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [MaxRecords 属性示例 (VB)](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [MaxRecords 属性示例 (VC++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
