---
title: Analysis Services DAX 属性 |Microsoft Docs
ms.date: 10/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 20a6df833f8c525c24abdf3bb51278d0067db951
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2018
ms.locfileid: "53071894"
---
# <a name="dax-properties"></a>DAX 属性
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

   Msmdsrv.ini 的 DAX 区域包含用于控制在 Analysis Services 中，某些查询行为例如 DAX 查询结果集中返回的行数的上限的设置。

  对于非常大的行集，例如 DirectQuery 模型中返回的行集，默认值 100 万行可能会不够。 就会知道是否需要调整限制如果收到此错误："外部数据源的查询的结果集已超出最大允许行数 1000000 行"。

若要增加上限，请指定 **MaxIntermediateRowSize** 配置设置。 需要手动将完整元素添加到配置文件的 DAX 区域中。 只有在添加设置之后，设置才会出现在该文件中。

## <a name="configuration-snippet"></a>配置代码段

```
<ConfigurationSettings>
. . .
<DAX>
  <PredicateCheckSpoolCardinalityThreshold>5000
  </PredicateCheckSpoolCardinalityThreshold>
  <DQ>
     <MaxIntermediateRowsetSize>1000000
     </MaxIntermediateRowsetSize>
  </DQ>
</DAX>
. . .
```

## <a name="property-descriptions"></a>属性说明

设置 |ReplTest1 |Description
--------|-------|-----------
MaxIntermediateRowsetSize | 1000000 | DAX 查询中返回的最大行数。 手动将此条目添加到 msmdsrv.ini 文件中，如果默认值过低，请增加值。
PredicateCheckSpoolCardinalityThreshold| 5000 | 这是一项高级属性，除非有 Microsoft 技术支持的指导，否则不应更改此属性。

有关更多服务器属性以及如何设置这些属性的详细信息，请参阅 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。
