---
description: Name 属性 (ADO MD)
title: 名称属性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Name
- CubeDef::Name
- Member::Name
- Catalog::Name
- Dimension::Name
- Name
- Axis::Name
- Hierarchy::Name
helpviewer_keywords:
- Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
author: rothja
ms.author: jroth
ms.openlocfilehash: 83207cd13db790d645bea146b2a031604e598256
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777946"
---
# <a name="name-property-ado-md"></a>Name 属性 (ADO MD)
指示对象的名称。  
  
## <a name="return-values"></a>返回值  
 返回一个 **字符串** ，并且为只读。  
  
## <a name="remarks"></a>备注  
 可以按序号引用检索对象的 **Name** 属性，之后可以按名称直接引用对象。 例如，如果 `cdf.CubeDefs(0).Name` 生成 "Bobs-sfpreviewcluster Video Store"，则可以将此 [CubeDef](./cubedef-object-ado-md.md) 称为 `cdf.CubeDefs("Bobs Video Store")` 。  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [轴对象 (ADO MD)](./axis-object-ado-md.md)  
        [目录对象 (ADO MD)](./catalog-object-ado-md.md)  
        [CubeDef 对象 (ADO MD)](./cubedef-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [维度对象 (ADO MD)](./dimension-object-ado-md.md)  
        [层次结构对象 (ADO MD)](./hierarchy-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [级别对象 (ADO MD)](./level-object-ado-md.md)  
        [成员对象 (ADO MD)](./member-object-ado-md.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [ (VB 的目录示例) ](./catalog-example-vb.md)   
 [标题属性 (ADO MD) ](./caption-property-ado-md.md)   
 [Description 属性 (ADO MD) ](./description-property-ado-md.md)   
 [UniqueName 属性 (ADO MD)](./uniquename-property-ado-md.md)