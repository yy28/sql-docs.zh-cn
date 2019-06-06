---
title: 密钥对象 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6dbbb81d53755032725ad71ff9bbf49b9beb2f1c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706473"
---
# <a name="key-object-adox"></a>项对象 (ADOX)
表示从数据库表的主键、 外，或唯一键字段。  
  
## <a name="remarks"></a>备注  
 下面的代码创建一个新**密钥**:  
  
```  
Dim obj As New Key  
```  
  
 使用属性和集合**密钥**对象，你可以：  
  
-   标识与密钥[名称](../../../ado/reference/adox-api/name-property-adox.md)属性。  
  
-   确定是否主键、 外，或使用唯一键[类型](../../../ado/reference/adox-api/type-property-key-adox.md)属性。  
  
-   访问密钥的数据库列[列](../../../ado/reference/adox-api/columns-collection-adox.md)集合。  
  
-   指定包含相关表的名称[RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md)属性。  
  
-   确定在删除或更新一个包含主键的执行的操作[DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md)并[UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md)属性。  
  
 本部分包含以下主题。  
  
-   [项对象属性、方法和事件](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [项 Append 方法、 密钥类型、 RelatedColumn、 RelatedTable 和 UpdateRule 属性示例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [列集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [项集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)
