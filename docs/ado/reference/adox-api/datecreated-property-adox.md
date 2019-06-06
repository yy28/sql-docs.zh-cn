---
title: DateCreated 属性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c2f20cbad4a83d17ae4255962d613652e4fb3794
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718942"
---
# <a name="datecreated-property-adox"></a>DateCreated 属性 (ADOX)
指示该对象的创建的日期。  
  
## <a name="return-values"></a>返回值  
 返回**变体**值，该值指定创建日期。 值为 null 如果**DateCreated**提供程序不支持。  
  
## <a name="remarks"></a>备注  
 **DateCreated**属性是新追加的对象为 null。 之后追加一个新[视图](../../../ado/reference/adox-api/view-object-adox.md)或[过程](../../../ado/reference/adox-api/procedure-object-adox.md)，则必须调用[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法[视图](../../../ado/reference/adox-api/views-collection-adox.md)或[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)要获取的值的集合**DateCreated**属性。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[过程对象 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[视图对象 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>请参阅  
 [DateCreated 和 DateModified 属性示例 (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified 属性 (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)
