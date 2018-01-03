---
title: "Count 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Collection::Count
helpviewer_keywords: Count property [ADO]
ms.assetid: da9ccd1f-d402-41a2-940c-45556fc5340d
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 186b8ace444c3e006c3978a1c8f2843bb422601f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="count-property-ado"></a>Count 属性 (ADO)
指示集合中的对象数。  
  
## <a name="return-value"></a>返回值  
 返回**长**值。  
  
## <a name="remarks"></a>Remarks  
 使用**计数**属性来确定在给定集合中对象数。  
  
 由于集合的成员计数从零开始，你应始终将循环零成员开始和结束值为**计数**减 1 的属性。 如果你正在使用 Microsoft Visual Basic 并想要循环访问集合的成员，而不会检查**计数**属性，请使用**每个...下一步**命令。  
  
 如果**计数**属性为零，集合中有任何对象。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [计数属性示例 (VB)](../../../ado/reference/ado-api/count-property-example-vb.md)   
 [计数属性示例 （VC + +）](../../../ado/reference/ado-api/count-property-example-vc.md)   
 [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
