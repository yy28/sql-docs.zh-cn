---
title: AssociationSet 元素 (CSDLBI) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 93e5ac4d-d7e8-490e-b775-28263a48cfcc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a7e165afc901b82d73f11f04fbb2c2cbb5402ac
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224887"
---
# <a name="associationset-element-csdlbi"></a>AssociationSet 元素 (CSDLBI)
  `AssociationSet` 元素是一种用于定义关联的复杂类型。 在 CSDLBI 数据模型中，关联是指两个表之间的关系。  
  
 必须为模型中的每个唯一关系指定一个 `AssociationSet`。 `AssociationSet` 通过使用 `Association` 元素来定义端点。 `AssociationSet` 元素还定义有关数据模型中的关系及其使用情况的元数据。  
  
## <a name="applicable-attributes"></a>适用的属性  
 下表列出了用于定义 `AssociationSet` 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|State|用户帐户控制|指示关联是否有效的字符串。 值由 State 元素定义。|  
|Hidden|否|指示关系是否可见的布尔值。 默认情况下，Hidden 的值为 `false`，表示所有关系在模型中均可见。|  
  
## <a name="state-element"></a>State 元素  
 `State` 元素是一种简单类型，说明关联是否处于活动状态，如果处于活动状态，则应在计算中使用；如果处于非活动状态，则必须显式在计算中引用。  
  
 如果有多个关联集连接两个实体，则只能将一个关联集标记为处于活动状态。 换言之，如果相同两个表之间具有两个关系，则只有一个关系可以处于活动状态。  
  
 下表列出了 `State` 元素的值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|在职|关联处于活动状态。|  
|Inactive|关联处于活动状态。|  
  
## <a name="example"></a>示例  
 **表格**  
  
 下面的示例显示 AdventureWorks 表格模型中的一个关系（在 CSDLBI 版本 1.1 中）。 关联标记为处于 Inactive（不活动）状态，因为有一个现有关系（在 OrderKey 与 Date 之间）。  
  
```  
<AssociationSet   
    Name="InternetSales_Date_Date_Date"  
    Association="Sandbox.InternetSales_Date_Date_Date">  
    <End EntitySet="InternetSales" />  
    <End EntitySet="DimDate" />  
<bi:AssociationSet State="Inactive" />  
</AssociationSet>  
  
```  
  
## <a name="example"></a>示例  
 **多维**  
  
 以下示例显示在 Contoso Operations 多维数据集中的 Sales 表和 Currency 表之间定义的关系。  
  
```  
<AssociationSet   
    Name ="Sales_Currency_Currency_Currency_Name2"  
    Association ="Sandbox.Sales_Currency_Currency_Currency_Name2">  
    <End EntitySet ="Sales" />  
    <End EntitySet ="Currency" />  
<bi:AssociationSet />  
</AssociationSet>  
```  
  
## <a name="see-also"></a>请参阅  
 [用于商业智能的 CSDL 注释技术参考](technical-reference-for-bi-annotations-to-csdl.md)  
  
  
