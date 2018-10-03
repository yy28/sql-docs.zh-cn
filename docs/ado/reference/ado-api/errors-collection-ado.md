---
title: 错误集合 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords:
- Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b595baf25a8b0f3982399c384c169c6af3f1cd81
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612225"
---
# <a name="errors-collection-ado"></a>错误集合 (ADO)
包含所有[错误](../../../ado/reference/ado-api/error-object.md)到单个提供程序相关的失败的响应中创建的对象。  
  
## <a name="remarks"></a>备注  
 任何涉及 ADO 对象的操作可以生成一个或多个提供程序错误。 每个错误发生时，一个或多个**错误**对象可以置于**错误**的集合[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。 当另一个 ADO 操作生成一个错误，**错误**清除集合，和一组新的**错误**对象可以置于**错误**集合。  
  
 每个**错误**对象都表示特定的提供程序错误，而不是 ADO 错误。 ADO 错误公开给运行时异常处理机制。 例如，在 Microsoft Visual Basic 中，特定于 ADO 的错误的匹配项将触发[onError](../../../ado/reference/rds-api/onerror-event-rds.md)事件并显示在**Err**对象。  
  
 不要生成错误的 ADO 操作不起任何作用**错误**集合。 使用[清除](../../../ado/reference/ado-api/clear-method-ado.md)方法来手动清除**错误**集合。  
  
 一套**错误**中的对象**错误**集合介绍发生以响应一条语句的所有错误。 枚举中的特定错误**错误**集合可以使您的错误处理例程可以更精确地确定的原因和错误的根源并采取适当措施来恢复。  
  
 某些属性和方法返回显示为警告**错误**中的对象**错误**集合但不是会停止程序执行。 在调用之前[重新同步](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)上的方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法**连接**对象，或者设置[筛选器](../../../ado/reference/ado-api/filter-property.md)属性**记录集**对象，请调用**清除**上的方法**错误**集合。 这样可以读取[计数](../../../ado/reference/ado-api/count-property-ado.md)的属性**错误**集合以测试是否返回警告。  
  
> [!NOTE]
>  请参阅**错误**单个 ADO 操作可以生成多个错误的方式的更多详细说明的主题。  
  
 本部分包含以下主题。  
  
-   [错误集合属性、 方法和事件](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [错误对象](../../../ado/reference/ado-api/error-object.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
