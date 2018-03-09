---
title: "– 属性 (ADOX) |Microsoft 文档"
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
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c7f405958cdd28e6dd4ae285c29ce806c2a61074
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="datecreated-property-adox"></a>– 属性 (ADOX)
指示创建对象时的日期。  
  
## <a name="return-values"></a>返回值  
 返回**Variant**值，该值指定创建日期。 值为 null 如果**时间**提供程序不支持。  
  
## <a name="remarks"></a>注释  
 **时间**属性是追加新的对象为 null。 之后追加一个新[视图](../../../ado/reference/adox-api/view-object-adox.md)或[过程](../../../ado/reference/adox-api/procedure-object-adox.md)，必须调用[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法[视图](../../../ado/reference/adox-api/views-collection-adox.md)或[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)若要获取的值的集合**时间**属性。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[过程对象 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[视图对象 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>另请参阅  
 [时间和 DateModified 属性示例 (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified 属性 (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)
