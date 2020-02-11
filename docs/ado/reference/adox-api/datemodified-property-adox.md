---
title: DateModified 属性（ADOX） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966500"
---
# <a name="datemodified-property-adox"></a>DateModified 属性 (ADOX)
指示上次修改对象的日期。  
  
## <a name="return-values"></a>返回值  
 返回指定修改日期的**变量**值。 如果提供程序不支持**DateModified** ，则该值为 null。  
  
## <a name="remarks"></a>备注  
 新追加的对象的**DateModified**属性为 null。 追加新的[视图](../../../ado/reference/adox-api/view-object-adox.md)或[过程](../../../ado/reference/adox-api/procedure-object-adox.md)之后，必须调用[视图](../../../ado/reference/adox-api/views-collection-adox.md)或[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)集合的[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法，以获取**DateModified**属性的值。  
  
## <a name="applies-to"></a>应用于  
  
||||  
|-|-|-|  
|[过程对象 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[视图对象 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>另请参阅  
 [DateCreated 和 DateModified 属性示例（VB）](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated 属性 (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
