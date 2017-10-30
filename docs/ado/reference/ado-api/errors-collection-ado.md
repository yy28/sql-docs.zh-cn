---
title: "错误集合 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords:
- Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 27ca46528314f34b769d505269ade0c73fb1b051
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="errors-collection-ado"></a>错误集合 (ADO)
包含所有[错误](../../../ado/reference/ado-api/error-object.md)到单个提供程序相关的失败的响应中创建的对象。  
  
## <a name="remarks"></a>注释  
 涉及 ADO 对象的任何操作可以生成一个或多个提供程序错误。 每个错误发生时，一个或多个**错误**对象可以放置在**错误**集合[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。 当另一个 ADO 操作生成错误，**错误**集合处于未选中状态，以及新的集**错误**对象可以放置在**错误**集合。  
  
 每个**错误**对象表示特定的提供程序错误，而不是 ADO 错误。 ADO 错误公开给运行时异常处理机制。 例如，在 Microsoft Visual Basic，ADO 特定错误的匹配项将触发[onError](../../../ado/reference/rds-api/onerror-event-rds.md)事件并显示在**Err**对象。  
  
 不生成错误的 ADO 操作产生任何影响**错误**集合。 使用[清除](../../../ado/reference/ado-api/clear-method-ado.md)方法手动清除**错误**集合。  
  
 一套**错误**中的对象**错误**集合描述单个语句的响应中出现的所有错误。 枚举中的特定错误**错误**集合使您的错误处理例程可以更精确地确定原因和源的错误，并采取适当措施来恢复。  
  
 某些属性和方法返回显示为警告**错误**中的对象**错误**集合但不是会停止对程序的执行。 在调用之前[重新同步](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法**连接**对象，或设置[筛选器](../../../ado/reference/ado-api/filter-property.md)属性**记录集**对象，请调用**清除**方法**错误**集合。 这样你可以阅读[计数](../../../ado/reference/ado-api/count-property-ado.md)属性**错误**集合以测试是否返回警告。  
  
> [!NOTE]
>  请参阅**错误**对象主题有关单个 ADO 操作可以生成多个错误的方式的更多详细说明。  
  
 本部分包含以下主题。  
  
-   [错误集合属性、 方法和事件](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [错误对象](../../../ado/reference/ado-api/error-object.md)   
 [附录 a： 提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)

