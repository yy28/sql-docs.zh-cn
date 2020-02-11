---
title: 定义半累加性行为 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- semiadditive
- Business Intelligence enhancements [Analysis Services], semiadditive behavior
- measures [Analysis Services], semiadditive
ms.assetid: b25726bc-728b-4601-ad87-9015c39dc615
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c72cc6b3798d790b4787cb5fcfe3e560b6580fc2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075541"
---
# <a name="define-semiadditive-behavior"></a>定义半累加性行为
  在很多业务方案中，半累加性度量值是非常常见的，它不在所有维度中统一进行聚合。 每个基于余额快照的多维数据集都会随着时间的推移而出现此问题。 您可以在用于处理证券、帐户余额、预算、人力资源、保险策略和法律事务以及很多其他业务领域的应用程序中找到这些快照。  
  
 通过在多维数据集中添加半累加性行为，可以为帐户类型属性的单个度量值或成员定义聚合方法。 如果多维数据集包含帐户维度，那么您可以基于该帐户类型来自动设置半累加性行为。  
  
 若要添加半累加性行为，请在多维数据集设计器中打开一个多维数据集，并从“多维数据集”菜单中选择 **“添加商业智能”** 。 在商业智能向导中，选择 **“选择增强功能”** 页上的 **“定义半累加性行为”** 选项。 然后，此向导将引导您完成相应的步骤，以标识哪些度量值有半累加性行为。  
  
 除了可用于标准版本的 LastChild 之外，其他的半累加行为仅可用于商业智能或企业版本。  
  
## <a name="define-semiadditive-behavior"></a>定义半累加性行为  
 在向导的 **“定义半累加性行为”** 页上，通过选择下列选项之一来选择如何定义半累加性：  
  
 **关闭半累加性行为**  
 从先前定义了半累加性行为的多维数据集中删除半累加性行为。 如果将它设置为以下聚合函数类型中的任何一个，则该选择将使度量值重置为 `SUM`：  
  
-   By Account  
  
-   Average of Children  
  
-   First Child  
  
-   Last Child  
  
-   Last Nonempty Child  
  
-   First Nonempty Child  
  
-   无  
  
 此选项不会更改使用常规聚合函数的度量值`Sum`： `Min`、 `Max`、 `Count`、或`Distinct``Count`。  
  
 **向导检测到包含半累加性成员的 "账户" 帐户维度。服务器将根据为每种帐户类型指定的半累加性行为聚合此维度的成员。**  
 导致系统将按“帐户”类型维度进行维度化的度量值组中的所有度量值设置为“按帐户”聚合函数，并且服务器将根据为每个帐户类型指定的半累加性行为聚合此维度的成员。  
  
> [!NOTE]  
>  如果向导检测到“帐户”类型维度，则默认情况下选择此选项。  
  
 **定义各个度量值的半累加性行为**  
 逐个选择每个度量值的半累加性行为。 默认设置是 `SUM` （完全累加）。  
  
> [!NOTE]  
>  如果向导没有检测到“帐户”类型维度，则默认情况下选择此选项。  
  
 对于每个度量值，可以从下表所描述的半累加性功能类型中进行选择。  
  
|半累加性函数|说明|  
|---------------------------|-----------------|  
|Average of Children|成员的聚合是其子级的平均。|  
|ByAccount|系统读取为帐户类型指定的半累加性行为。|  
|Count|聚合是成员的计数。|  
|Distinct Count|聚合是唯一成员的计数。|  
|First Child|将成员值认定为其沿时间维度的第一个子级的值。|  
|FirstNonEmpty|将成员值认定为其包含数据的沿时间维度的第一个子级的值。|  
|LastChild|将成员值认定为其沿时间维度的最后一个子级的值。|  
|LastNonEmpty|将成员值认定为其包含数据的沿时间维度的最后一个子级的值。|  
|Max|应用标准的最大值聚合函数。|  
|Min|应用标准的最小值聚合函数。|  
|无|不应用聚合。|  
|SUM|应用标准的求和函数。|  
  
 完成向导时，将覆盖任何现有的半累加性行为。  
  
  
