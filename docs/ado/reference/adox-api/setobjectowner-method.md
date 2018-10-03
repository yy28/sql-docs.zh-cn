---
title: SetObjectOwner 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::SetObjectOwner
- _Catalog::raw_SetObjectOwner
helpviewer_keywords:
- SetObjectOwner method [ADOX]
ms.assetid: e5170a37-9d6e-43db-bfb6-9b6631fa3048
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43f325382cc556d75d7ab08c5b3dbdc94f68704f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617255"
---
# <a name="setobjectowner-method"></a>SetObjectOwner 方法
指定对象中的对象所有者[目录](../../../ado/reference/adox-api/catalog-object-adox.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Catalog.SetObjectOwner ObjectName, ObjectType, OwnerName [,ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parameters  
 *ObjectName*  
 一个**字符串**值，该值指定要为其指定所有者的对象的名称。  
  
 *ObjectType*  
 一个**长**值，它可以是其中一个的[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)指定所有者类型的常量。  
  
 *OwnerName*  
 一个**字符串**值，该值指定[名称](../../../ado/reference/adox-api/name-property-adox.md)的[用户](../../../ado/reference/adox-api/user-object-adox.md)或者[组](../../../ado/reference/adox-api/group-object-adox.md)以拥有的对象。  
  
 *ObjectTypeId*  
 可选。 一个**变体**值，该值指定未由 OLE DB 规范定义的提供程序对象类型的 GUID。 此参数是必需的如果*ObjectType*设置为**adPermObjProviderSpecific**; 否则为不使用它。  
  
## <a name="remarks"></a>备注  
 如果提供程序不支持指定对象所有者，将会出错。  
  
## <a name="applies-to"></a>适用范围  
 [目录对象 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>请参阅  
 [GetObjectOwner 和 SetObjectOwner 方法示例 (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [GetObjectOwner 方法 (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)
