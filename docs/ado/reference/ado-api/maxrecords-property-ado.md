---
description: MaxRecords 属性 (ADO)
title: " (ADO) 的 MaxRecords 属性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 31870c4df71b20c162f95f1f1d942dde63885227
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990638"
---
# <a name="maxrecords-property-ado"></a>MaxRecords 属性 (ADO)
指示要从查询返回到 [记录集](./recordset-object-ado.md) 的最大记录数。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个 **长整型** 值，该值指示要返回的最大记录数。 默认值为零 (**0**) ，表示没有限制。  
  
## <a name="remarks"></a>注解  
 使用 **MaxRecords** 属性可限制访问接口从数据源返回的记录数。 此属性的默认设置为零，表示提供程序返回所有请求的记录。  
  
 当**记录集**关闭时， **MaxRecords**属性是可读/写的。  
  
## <a name="applies-to"></a>适用于  
 [记录集对象 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [MaxRecords 属性示例 (VB) ](./maxrecords-property-example-vb.md)   
 [MaxRecords 属性示例 (VC++)](./maxrecords-property-example-vc.md)