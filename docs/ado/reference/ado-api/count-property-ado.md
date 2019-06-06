---
title: Count 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Count
helpviewer_keywords:
- Count property [ADO]
ms.assetid: da9ccd1f-d402-41a2-940c-45556fc5340d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 10f531b601e44f346e27b52e40e6591457055ee8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698459"
---
# <a name="count-property-ado"></a>Count 属性 (ADO)
指示集合中的对象数。  
  
## <a name="return-value"></a>返回值  
 返回**长**值。  
  
## <a name="remarks"></a>备注  
 使用**计数**属性来确定给定集合中的对象数。  
  
 由于对集合成员的编号从零开始，应始终将循环从零个成员开始和结束值为**计数**减 1 的属性。 如果你使用的 Microsoft Visual Basic 并想要循环访问集合的成员，而不检查**计数**属性，请使用**为每个...下一步**命令。  
  
 如果**计数**属性为零，则集合中没有任何对象。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[轴集合 (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[列集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs 集合 (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[维度集合 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[错误集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[组集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[层次结构集合 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[项集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[级别集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[成员集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[位置集合 (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[过程集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[用户集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>请参阅  
 [Count 属性示例 (VB)](../../../ado/reference/ado-api/count-property-example-vb.md)   
 [Count 属性示例 （VC + +）](../../../ado/reference/ado-api/count-property-example-vc.md)   
 [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
