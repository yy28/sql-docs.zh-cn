---
title: 单元集对象 (ADO MD) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset
helpviewer_keywords:
- Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6437c17c80c85e535f6b1807f68c2755e1362d3c
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35283386"
---
# <a name="cellset-object-ado-md"></a>单元集对象 (ADO MD)
表示多维查询的结果。 它是从多维数据集或其他单元集中选定单元格的集合。  
  
## <a name="remarks"></a>Remarks  
 中的数据**单元集**检索使用直接的、 类似数组的访问。 您可以深化到特定的成员，以获取有关该成员的数据。 例如，下面的代码返回的第一个成员的标题中的第一个位置上名为单元集的第一个轴`cst`:  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>Remarks  
 没有单元集内的当前单元格的概念。 相反，[项](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)属性检索特定[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)从单元集的对象。 自变量**项**属性确定检索的单元格。 你可以指定单元格的唯一序号值。 您还可以通过使用其的单元集的每个轴的位置编号检索单元格。 有关检索单元格的详细信息，请参阅[项](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)属性。  
  
 使用集合、 方法和属性的**单元集**对象，你可以执行以下操作：  
  
-   将关联的打开连接使用**单元集**对象通过设置其[ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)属性。  
  
-   执行并检索与多维查询的结果[打开](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法。  
  
-   检索**单元格**从**单元集**与[项](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)属性。  
  
-   返回[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)定义的对象**单元集**与[轴](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)集合。  
  
-   检索用来筛选数据中的维度的信息**单元集**与[FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md)属性。  
  
-   返回或指定用于定义查询**单元集**与[源](../../../ado/reference/ado-md-api/source-property-ado-md.md)属性。  
  
-   返回的当前状态**单元集**（打开、 关闭状态，执行，或连接） 与[状态](../../../ado/reference/ado-md-api/state-property-ado-md.md)属性。  
  
-   关闭已打开**单元集**与[关闭](../../../ado/reference/ado-md-api/close-method-ado-md.md)方法。  
  
-   有关检索提供程序特定的信息**单元集**用标准 ADO[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 本部分包含以下主题。  
  
-   [属性、 方法和事件](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [单元集示例 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [轴集合 (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [单元格对象 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
