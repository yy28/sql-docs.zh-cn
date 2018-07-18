---
title: ASSL XML 约定 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d248cc39e20869752deb67c0c84c8b0aca6aafd0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279893"
---
# <a name="assl-xml-conventions"></a>ASSL XML 约定
  Analysis Services 脚本语言 (ASSL) 将对象层次结构表示为一组元素类型，其中的每个元素类型定义了可包含的子元素。  
  
 ASSL 使用以下 XML 约定来表示对象层次结构：  
  
-   标准 XML 特性（例如“xml:lang”）除外，所有对象和属性都表示为元素。  
  
-   元素名称和枚举值遵循 Microsoft.NET Framework 命名约定的 Pascal 大小写格式且没有下划线字符。  
  
-   保留所有值的大小写。 枚举值也区分大小写。  
  
 除了此约定列表之外，Analysis Services 还遵循有关基数、继承、空格、数据类型和默认值的特定约定。  
  
## <a name="cardinality"></a>基数  
 当某个元素有一个大于 1 的基数时，将存在一个封装此元素的 XML 元素集合。 该集合的名称使用集合中所包含元素的复数形式。 例如，以下 XML 片段表示 `Dimensions` 元素内的 `Database` 集合：  
  
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
 存在具有重叠但有显著不同的属性集的不同对象时，会使用继承。 这种重叠但又不同的对象示例有虚拟多维数据集、链接多维数据集和常规多维数据集。 对于重叠但又不同的对象，Analysis Services 会使用 XML 实例命名空间的标准 `type` 属性来表示继承。 例如，以下 XML 片段显示 `type` 属性如何标识 `Cube` 元素是继承自常规多维数据集还是虚拟多维数据集：  
  
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
  
 当多个类型具有同一名称的属性时，通常不使用继承。 例如，`Name` 和 `ID` 属性出现在许多元素中，但这些属性尚未提升为抽象类型。  
  
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
  
 `Int`  
 -231 到 231 – 1 范围内的整数值。  
  
 `Long`  
 -263 到 263 – 1 范围内的整数值。  
  
 `String`  
 符合以下全局规则的字符串值：  
  
-   去除控制字符。  
  
-   删除前导空格和尾随空格。  
  
-   保留内部空格。  
  
 `Name` 和 `ID` 属性对字符串元素中的有效字符具有特殊限制。 有关其他信息`Name`并`ID`约定，请参阅[ASSL 对象和对象特征](assl-objects-and-object-characteristics.md)。  
  
 `DateTime`  
 一个`DateTime`从.NET Framework 的结构。 `DateTime` 值不能为 NULL。 `DataTime` 数据类型支持的最早日期为 1601 年 1 月 1 日，程序员可将该日期作为 `DateTime.MinValue`。 该最早支持日期指示缺少 `DateTime` 值。  
  
 `Boolean`  
 仅具有两个值的枚举，例如 {true, false} 或 {0, 1}。  
  
## <a name="default-values"></a>默认值  
 Analysis Services 使用下表所列的默认值。  
  
|XML 数据类型|默认值|  
|-------------------|-------------------|  
|`Boolean`|False|  
|`String`|""（空字符串）|  
|`Integer` 或 `Long`|0（零）|  
|`Timestamp`|12:00:00 AM，0001 年 1 月 1 日 (对应于.NET Frameworks`System.DateTime`与 0 刻度)|  
  
 存在但为空的元素被解释为具有 Null 字符串值，而非默认值。  
  
### <a name="inherited-defaults"></a>继承的默认值  
 对象上指定的某些属性可以向子对象或后代对象中的同一属性提供默认值。 例如，`Cube.StorageMode` 可向 `Partition.StorageMode` 提供默认值。 Analysis Services 应用于继承默认值的规则如下所示：  
  
-   在 XML 中，如果子对象的属性为 Null，则该属性的值将默认为继承的值。 但当您从服务器查询值时，服务器将会返回值为空的 XML 元素。  
  
-   无法通过编程方式来确定子对象属性是直接在子对象上设置的，还是直接继承的。  
  
 某些元素已定义当元素缺少时要应用的默认值。 例如，以下 XML 片段中的 `Dimension` 元素是等效的，即使一个 `Dimension` 元素包含 `Visible` 元素，而另一个 `Dimension` 元素不包含。  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 有关继承的默认值的详细信息，请参阅[ASSL 对象和对象特征](assl-objects-and-object-characteristics.md)。  
  
  
