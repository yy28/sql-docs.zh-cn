---
title: "ASSL XML 约定 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- whitespace [Analysis Services Scripting Language]
- trailing whitespace
- XSD data types [Analysis Services Scripting Language]
- inheritance [Analysis Services Scripting Language]
- cardinality [Analysis Services Scripting Language]
- white space [Analysis Services Scripting Language]
- ASSL, XML conventions
- defaults [Analysis Services Scripting Language]
- leading whitespace
- Analysis Services Scripting Language, XML conventions
- XML [Analysis Services Scripting Language]
- hierarchies [Analysis Services Scripting Language]
- inherited defaults [Analysis Services Scripting Language]
ms.assetid: bce4edad-4420-41ce-9672-8c00c5c0dec6
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a8cd244f64d45ff81ff51cba6b528c81ba743ff1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="assl-xml-conventions"></a>ASSL XML 约定
  Analysis Services 脚本语言 (ASSL) 将对象层次结构表示为一组元素类型，其中的每个元素类型定义了可包含的子元素。  
  
 ASSL 使用以下 XML 约定来表示对象层次结构：  
  
-   标准 XML 特性（例如“xml:lang”）除外，所有对象和属性都表示为元素。  
  
-   元素名称和枚举值遵循 Microsoft.NET Framework 命名约定的 Pascal 大小写与没有下划线。  
  
-   保留所有值的大小写。 枚举值也区分大小写。  
  
 除了此约定列表之外，Analysis Services 还遵循有关基数、继承、空格、数据类型和默认值的特定约定。  
  
## <a name="cardinality"></a>基数  
 当某个元素有一个大于 1 的基数时，将存在一个封装此元素的 XML 元素集合。 该集合的名称使用集合中所包含元素的复数形式。 例如，以下 XML 片段表示**维度**内的集合，**数据库**元素：  
  
 `<Database>`  
  
 `…`  
  
 `<Dimensions>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `</Dimensions>`  
  
 `</Database>`  
  
 ``  
  
 元素的出现顺序并不重要。  
  
## <a name="inheritance"></a>继承  
 存在具有重叠但有显著不同的属性集的不同对象时，会使用继承。 这种重叠但又不同的对象示例有虚拟多维数据集、链接多维数据集和常规多维数据集。 对于重叠但不同的对象，Analysis Services 使用标准**类型**从 XML 实例 Namespace，以指示继承的属性。 例如，下面的 XML 片段说明如何**类型**特性标识是否**多维数据集**元素继承从常规多维数据集或虚拟多维数据集：  
  
 `<Cubes>`  
  
 `<Cube xsi:type=”RegularCube”>`  
  
 `<Name>Sales</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `<Cube xsi:type=”VirtualCube”>`  
  
 `<Name>SalesAndInventory</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `</Cubes>`  
  
 ``  
  
 当多个类型具有同一名称的属性时，通常不使用继承。 例如，**名称**和**ID**属性出现在许多元素，但这些属性不已提升为抽象类型。  
  
## <a name="whitespace"></a>空格  
 将保留元素值中的空格。 但会始终删除前导空格和尾随空格。 例如，下面的元素具有相同的文本，但该文本内的空格数量不同，因此，会将它们视为具有不同的值：  
  
 `<Description>My text<Description>`  
  
 `<Description>My  text<Description>`  
  
 ``  
  
 然而，下面的元素仅前导空格和尾随空格不同，因此，会将它们视为具有等效值：  
  
 `<Description>My text<Description>`  
  
 `<Description>  My text  <Description>`  
  
 ``  
  
## <a name="data-types"></a>数据类型  
 Analysis Services 使用以下标准 XML 架构定义语言 (XSD) 数据类型：  
  
 **Int**  
 -231 到 231 – 1 范围内的整数值。  
  
 **Long**  
 -263 到 263 – 1 范围内的整数值。  
  
 **字符串**  
 符合以下全局规则的字符串值：  
  
-   去除控制字符。  
  
-   删除前导空格和尾随空格。  
  
-   保留内部空格。  
  
 **名称**和**ID**属性在字符串元素中的有效字符上有特殊限制。 有关其他信息**名称**和**ID**约定，请参阅[ASSL 对象和对象特征](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)。  
  
 **DateTime**  
 A **DateTime**在.NET Framework 中的结构。 A **DateTime**值不能为 NULL。 支持的最早日期**DataTime**数据类型是 1601 年 1 月 1 日，这是供作为程序员**DateTime.MinValue**。 最低支持的日期指示**DateTime**值已丢失。  
  
 **Boolean**  
 仅具有两个值的枚举，例如 {true, false} 或 {0, 1}。  
  
## <a name="default-values"></a>默认值  
 Analysis Services 使用下表所列的默认值。  
  
|XML 数据类型|默认值|  
|-------------------|-------------------|  
|**Boolean**|False|  
|**字符串**|""（空字符串）|  
|**整数**或**长**|0（零）|  
|**时间戳**|12:00:00 AM，0001 年 1 月 1 日 (对应于.NET 框架**System.DateTime** 0 时钟周期)|  
  
 存在但为空的元素被解释为具有 Null 字符串值，而非默认值。  
  
### <a name="inherited-defaults"></a>继承的默认值  
 对象上指定的某些属性可以向子对象或后代对象中的同一属性提供默认值。 例如， **Cube.StorageMode**提供的默认值为**Partition.StorageMode**。 Analysis Services 应用于继承默认值的规则如下所示：  
  
-   在 XML 中，如果子对象的属性为 Null，则该属性的值将默认为继承的值。 但当您从服务器查询值时，服务器将会返回值为空的 XML 元素。  
  
-   无法通过编程方式来确定子对象属性是直接在子对象上设置的，还是直接继承的。  
  
 某些元素已定义当元素缺少时要应用的默认值。 例如，**维度**以下 XML 片段中的元素相等，即使一个**维度**元素包含**可见**元素，但是其他**维度**元素不一样。  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 继承的默认设置的详细信息，请参阅[ASSL 对象和对象特征](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)。  
  
  

