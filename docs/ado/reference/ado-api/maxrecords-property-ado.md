---
title: MaxRecords 属性（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b9e4beaaa4b38a26089d1136d1b32090ea12231f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82754379"
---
# <a name="maxrecords-property-ado"></a>MaxRecords 属性 (ADO)
指示要从查询返回到[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)的最大记录数。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个**长整型**值，该值指示要返回的最大记录数。 默认值为零（**0**），表示没有限制。  
  
## <a name="remarks"></a>备注  
 使用**MaxRecords**属性可限制访问接口从数据源返回的记录数。 此属性的默认设置为零，表示提供程序返回所有请求的记录。  
  
 当**记录集**关闭时， **MaxRecords**属性是可读/写的。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [MaxRecords 属性示例（VB）](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [MaxRecords 属性示例 (VC++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
