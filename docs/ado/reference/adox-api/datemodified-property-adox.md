---
title: "DateModified 属性 (ADOX) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Table::get_DateModified
- _Table::DateModified
- _Table::GetDateModified
helpviewer_keywords:
- DateModified property [ADOX]
ms.assetid: fed09266-1547-4bda-9088-c254d81cc738
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 733de516ee160bb26cba4568cbe34b76277e511d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="datemodified-property-adox"></a>DateModified 属性 (ADOX)
指示对象上次修改日期。  
  
## <a name="return-values"></a>返回值  
 返回**Variant**值，该值指定修改日期。 值为 null 如果**DateModified**提供程序不支持。  
  
## <a name="remarks"></a>注释  
 **DateModified**属性是追加新的对象为 null。 之后追加一个新[视图](../../../ado/reference/adox-api/view-object-adox.md)或[过程](../../../ado/reference/adox-api/procedure-object-adox.md)，必须调用[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法[视图](../../../ado/reference/adox-api/views-collection-adox.md)或[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)若要获取的值的集合**DateModified**属性。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[过程对象 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[视图对象 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>另请参阅  
 [时间和 DateModified 属性示例 (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated 属性 (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
