---
title: "DAX 属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: aa928dc5-d00d-4f8a-80b9-7e6973d2196c
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a4a47254b6836b50023be16045aaa388e3aaac47
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="dax-properties"></a>DAX 属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
msmdsrv.ini 的 DAX 区域包含用于控制 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中某些查询行为的设置，例如 DAX 查询结果集中返回行数量的上限。

  对于非常大的行集，例如 DirectQuery 模型中返回的行集，默认值 100 万行可能会不够。 如果出现这个错误：“外部数据源的查询结果集已超过了允许的最大行数(1000000) 行”，你就知道是否需要调整限制。

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

设置 |“值” |Description
--------|-------|-----------
MaxIntermediateRowsetSize | 1000000 | DAX 查询中返回的最大行数。 手动将此条目添加到 msmdsrv.ini 文件中，如果默认值过低，请增加值。
PredicateCheckSpoolCardinalityThreshold| 5000 | 这是一项高级属性，除非有 Microsoft 技术支持的指导，否则不应更改此属性。

有关更多服务器属性以及如何设置这些属性的详细信息，请参阅 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。
