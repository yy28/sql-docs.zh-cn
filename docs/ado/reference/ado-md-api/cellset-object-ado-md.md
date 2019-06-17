---
title: 单元集对象 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset
helpviewer_keywords:
- Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 52ede9c21077c81dd1bd90f12acbfc3dff796d50
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66709495"
---
# <a name="cellset-object-ado-md"></a>单元集对象 (ADO MD)
表示多维查询的结果。 它是从多维数据集或其他单元集中选择的单元的集合。  
  
## <a name="remarks"></a>备注  
 中的数据**单元集**检索使用直接的类似数组的访问。 您可以深化到特定成员，才能获取有关该成员的数据。 例如，下面的代码返回的第一个成员的标题中的第一个位置上名为单元集的第一个轴`cst`:  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>备注  
 集中的单元格的当前单元格没有概念。 相反，[项](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)属性检索特定[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)从单元集对象。 参数**项**属性确定要检索的单元格。 您可以指定单元格的唯一的序号值。 此外可以通过使用其在单元集中每个轴的位置编号检索单元格。 检索单元格的详细信息，请参阅[项](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)属性。  
  
 使用集合、 方法和属性的**单元集**对象，您可以执行以下操作：  
  
-   将与打开的连接相关联**单元集**对象通过设置其[ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)属性。  
  
-   执行和检索多维查询的结果[打开](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法。  
  
-   检索**单元格**从**单元集**与[项](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)属性。  
  
-   返回[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)对象以定义**单元集**与[轴](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)集合。  
  
-   检索用于筛选中的数据维度的信息**单元集**与[FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md)属性。  
  
-   返回或指定用于定义查询**单元集**与[源](../../../ado/reference/ado-md-api/source-property-ado-md.md)属性。  
  
-   返回的当前状态**单元集**（打开、 关闭状态，执行，或连接） 与[状态](../../../ado/reference/ado-md-api/state-property-ado-md.md)属性。  
  
-   关闭已打开**单元集**与[关闭](../../../ado/reference/ado-md-api/close-method-ado-md.md)方法。  
  
-   检索有关特定于提供程序的信息**单元集**与标准的 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [单元集示例 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [轴集合 (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Cell 对象 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
