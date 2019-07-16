---
title: DateModified 属性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateModified
- _Table::DateModified
- _Table::GetDateModified
helpviewer_keywords:
- DateModified property [ADOX]
ms.assetid: fed09266-1547-4bda-9088-c254d81cc738
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cc41c630b8201651e933f5d6538e6887e7933c95
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966500"
---
# <a name="datemodified-property-adox"></a>DateModified 属性 (ADOX)
指示该对象的上次修改的日期。  
  
## <a name="return-values"></a>返回值  
 返回**变体**值，该值指定修改日期。 值为 null 如果**DateModified**提供程序不支持。  
  
## <a name="remarks"></a>备注  
 **DateModified**属性是新追加的对象为 null。 之后追加一个新[视图](../../../ado/reference/adox-api/view-object-adox.md)或[过程](../../../ado/reference/adox-api/procedure-object-adox.md)，则必须调用[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法[视图](../../../ado/reference/adox-api/views-collection-adox.md)或[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)要获取的值的集合**DateModified**属性。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[过程对象 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[视图对象 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>请参阅  
 [DateCreated 和 DateModified 属性示例 (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated 属性 (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
