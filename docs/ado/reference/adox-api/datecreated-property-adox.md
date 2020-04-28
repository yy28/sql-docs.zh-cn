---
title: DateCreated 属性（ADOX） |Microsoft Docs
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
ms.openlocfilehash: 0151b6388a19fc95227cbfa55a571e0a797d0acc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966573"
---
# <a name="datecreated-property-adox"></a>DateCreated 属性 (ADOX)
指示对象的创建日期。  
  
## <a name="return-values"></a>返回值  
 返回指定创建日期的**变量**值。 如果提供程序不支持**DateCreated** ，则该值为 null。  
  
## <a name="remarks"></a>备注  
 新追加的对象的**DateCreated**属性为 null。 追加新的[视图](../../../ado/reference/adox-api/view-object-adox.md)或[过程](../../../ado/reference/adox-api/procedure-object-adox.md)之后，必须调用[视图](../../../ado/reference/adox-api/views-collection-adox.md)或[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)集合的[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法，以获取**DateCreated**属性的值。  
  
## <a name="applies-to"></a>应用于  
  
||||  
|-|-|-|  
|[过程对象 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[视图对象 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>另请参阅  
 [DateCreated 和 DateModified 属性示例（VB）](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified 属性 (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)
