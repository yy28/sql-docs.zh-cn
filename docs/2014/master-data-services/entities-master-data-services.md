---
title: 实体 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], about entities
- entities [Master Data Services]
ms.assetid: 0af057d5-6b73-472b-99eb-9f5eb61a9b5b
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: bb54250b1be15916055dd59a3f2e6d37330d5d93
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800909"
---
# <a name="entities-master-data-services"></a>实体 (Master Data Services)
  实体是 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 模型中包含的对象。 每个实体都包含成员，它们是您管理的主数据的行。  
  
## <a name="how-many-entities-are-appropriate"></a>多少实体比较合适？  
 模型可以包含想要管理的任意多个实体。 每个实体应将相似类型的数据分组。 例如，您可能希望将一个实体用于您的所有公司帐户，或将一个实体用于雇员的主列表。  
  
 通常，有一个或多个中心实体对于您的业务非常重要，它们与模型中的其他对象关联。 例如，在 Product 模型中，可能有一个名为 Product 的中心实体和与 Product 实体关联的名为 Subcategory 和 Category 的实体。 但是，您不需要一定有中心实体。 根据您的需要，可能希望有几个同等重要的实体。  
  
## <a name="how-entities-relate-to-other-model-objects"></a>实体如何与其他模型对象关联  
 您可以将实体看作包含主数据的一个表，其中行表示成员，列表示属性。  
  
 ![表示为表的 Master Data Services 实体](../../2014/master-data-services/media/mds-conc-entity-table.gif "Master Data Services Entity Represented as Table")  
  
 使用要管理的主数据的列表填充该实体。  
  
 实体可用于生成派生层次结构，它们是基于多个实体的基于级别的层次结构。 有关详细信息，请参阅 [派生层次结构 (Master Data Services)](derived-hierarchies-master-data-services.md)。  
  
 还允许实体包含显示层次结构（基于单个实体的不规则结构）和集合（成员子集的一次性组合）。 有关详细信息，请参阅[显式层次结构 (Master Data Services)](../../2014/master-data-services/explicit-hierarchies-master-data-services.md) 和[集合 (Master Data Services)](../../2014/master-data-services/collections-master-data-services.md)。  
  
## <a name="using-entities-as-constrained-lists"></a>将实体用作受限制列表  
 用户将属性分配给实体中的成员时，可以从值的受限制列表中选择它们。 为此，您使用一个实体来填充该属性的值列表。 这称为基于域的属性。 有关详细信息，请参阅[基于域的属性 (Master Data Services)](../../2014/master-data-services/domain-based-attributes-master-data-services.md)。  
  
## <a name="base-entities"></a>基实体  
 在模型中浏览对象时，基实体是用户的起始点。 基实体确定当用户打开 **“资源管理器”** 功能区域并单击菜单栏上的 **“资源管理器”** 时屏幕的布局。 要将实体指定为基实体，请导航到 **“系统管理”** 功能区域。 在 **“模型视图”** 页中，将实体从右侧的树控件拖到左侧树控件中的模型名称。  
  
## <a name="entity-security"></a>实体安全性  
 可以授予用户对实体（包括相关模型对象）的权限。 有关详细信息，请参阅[实体权限 (Master Data Services)](../../2014/master-data-services/entity-permissions-master-data-services.md)。  
  
## <a name="entity-examples"></a>实体示例  
 下面的示例显示了这些属性的实体：名称、 代码、 Subcategory、 StandardCost、 ListPrice 和 FilePhoto。 这些属性描述成员。 每个成员由一行属性值表示。  
  
 ![自行车产品实体表](../../2014/master-data-services/media/mds-conc-entity-table-w-data.gif "Bike Product Entity Table")  
  
 在下面的示例中，Product 实体是中心实体。 Subcategory 实体是 Product 实体的基于域的属性。 Category 实体是 Subcategory 实体的基于域的属性。 StandardCost 和 ListPrice 是 Product 实体的自由格式的属性，FilePhoto 是 Product 实体的文件属性。  
  
 ![产品实体树结构](../../2014/master-data-services/media/mds-conc-entity-ui.gif "Product Entity Tree Structure")  
  
> [!NOTE]  
>  这是基于 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 用户界面 (UI) 的一个示例。 树状层次结构显示实体和基于域的属性之间的关系。 它旨在显示关系而不是表示重要性级别。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|创建新实体。|[创建实体 (Master Data Services)](../../2014/master-data-services/create-an-entity-master-data-services.md)|  
|指定一个实体可以包含显式层次结构和集合。|[为显式层次结构和集合启用实体&#40;Master Data Services&#41;](../../2014/master-data-services/enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md)|  
|更改现有实体的名称。|[更改实体名称&#40;Master Data Services&#41;](edit-an-entity-master-data-services.md)|  
|删除现有实体。|[删除实体 (Master Data Services)](../../2014/master-data-services/delete-an-entity-master-data-services.md)|  
|将权限分配给实体。|[分配模型对象权限 (Master Data Services)](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [模型 (Master Data Services)](../../2014/master-data-services/models-master-data-services.md)  
  
-   [成员 (Master Data Services)](../../2014/master-data-services/members-master-data-services.md)  
  
-   [属性 (Master Data Services)](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
