---
title: 属性 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- free-form attributes [Master Data Services]
- attributes [Master Data Services], about attributes
- attributes [Master Data Services], file attributes
- file attributes [Master Data Services]
- attributes [Master Data Services], free-form attributes
- attributes [Master Data Services]
ms.assetid: 95ecb75f-c559-41c3-933c-40ae60a4c2fd
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 430c4075a01777020ae2edc7014e94cf03e9d034
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972187"
---
# <a name="attributes-master-data-services"></a>属性 (Master Data Services)
  属性是 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实体中包含的对象。 属性值描述实体的成员。 属性可用于描述叶成员、合并成员或集合。  
  
## <a name="how-attributes-relate-to-other-model-objects"></a>属性如何与其他模型对象关联  
 您可以将属性视作实体表中的列。 属性值是用于描述特定成员的值。  
  
 ![表示为表的 Master Data Services 实体](../../2014/master-data-services/media/mds-conc-entity-table.gif "表示为表的 Master Data Services 实体")  
  
 创建包含很多属性的实体时，可以将属性组织为属性组。 有关详细信息，请参阅 [属性组 (Master Data Services)](attribute-groups-master-data-services.md)。  
  
## <a name="required-attributes"></a>必需的属性  
 创建实体时，将自动创建 Name 和 Code 属性。 Code 需要一个值，并且必须在实体中是唯一的。 不能删除 Name 和 Code 属性。  
  
## <a name="attribute-types"></a>属性类型  
 有三种类型的属性：  
  
-   自由格式的属性，允许针对文本、数字、日期或链接的自由格式的输入。  
  
-   基于域的属性，由实体填充。 有关详细信息，请参阅 [基于域的属性 (Master Data Services)](../../2014/master-data-services/domain-based-attributes-master-data-services.md)。  
  
-   文件属性，用于存储文件、文档或图像。 文件属性旨在通过要求文件具有特定的扩展名，帮助确保数据的一致性。 文件属性不一定能够防止恶意用户上载不同类型的文件。  
  
### <a name="numeric-free-form-attributes"></a>数字自由格式属性  
 数字自由格式属性值需要特殊处理，因为它们被限制为 **SqlDouble** 值类型。  
  
 默认情况下， **SqlDouble** 值包含 15 个小数位数的精度，尽管它在内部维护最大 17 位的精度。 浮点数的精度具有以下若干影响：  
  
-   对于特定精度，看起来相等的两个浮点数在进行比较时可能不相等，因为其最小有效位不同。  
  
-   在使用小数时，使用浮点数的算术或比较运算不一定产生相同结果，因为浮点数可能无法精确表示小数。  
  
-   如果包含浮点数，值可能无法“往返转换”。** 如果某一运算将原始浮点数转换为其他形式，而相反运算将已转换形式转换回浮点数，并且最终生成的浮点数与原始浮点数相等，则值被认为是往返转换。 因为在转换过程中一个或多个最小有效位缺失或更改，所以该往返转换可能失败。  
  
## <a name="attribute-examples"></a>属性示例  
 在下面的示例中，实体具有 Name、Code、Subcategory、StandardCost、ListPrice 和 FilePhoto 属性。 这些属性描述成员。 每个成员由一行属性值表示。  
  
 ![自行车产品实体表](../../2014/master-data-services/media/mds-conc-entity-table-w-data.gif "自行车产品实体表")  
  
 在下面的示例中，Product 实体包含：  
  
-   Name、Code、StandardCost 和 ListPrice 的自由格式属性。  
  
-   Subcategory 的基于域的属性。  
  
-   FilePhoto 的文件属性。  
  
 Subcategory 是用作 Product 的基于域的属性的实体。 Category 是用作 Subcategory 的基于域的属性的实体。 与 Product 实体一样，Category 和 Subcategory 实体各自包含默认 Name 和 Code 属性。  
  
 ![产品实体树结构](../../2014/master-data-services/media/mds-conc-entity-ui.gif "产品实体树结构")  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|创建新的自由格式的文本属性。|[创建文本属性 (Master Data Services)](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)|  
|创建新的自由格式的数字属性。|[创建数字属性 (Master Data Services)](../../2014/master-data-services/create-a-numeric-attribute-master-data-services.md)|  
|创建新的自由格式的链接属性。|[创建链接属性 (Master Data Services)](../../2014/master-data-services/create-a-link-attribute-master-data-services.md)|  
|创建新的文件属性。|[创建文件属性 (Master Data Services)](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)|  
|创建新的基于域的属性。|[创建基于域的属性 (Master Data Services)](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|更改现有属性的名称。|[更改属性名称 &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)|  
|向更改跟踪组添加现有属性。|[向更改跟踪组添加属性 (Master Data Services)](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)|  
|删除现有属性。|[删除属性 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-master-data-services.md)|  
|更改属性的顺序。|[更改属性的顺序](../../2014/master-data-services/change-the-order-of-attributes.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [基于域的属性 (Master Data Services)](../../2014/master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [属性组 (Master Data Services)](attribute-groups-master-data-services.md)  
  
-   [成员 &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)  
  
-   [叶权限 (Master Data Services)](../../2014/master-data-services/leaf-permissions-master-data-services.md)  
  
-   [&#40;Master Data Services 的合并权限&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)  
  
  
