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
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: aa928dc5-d00d-4f8a-80b9-7e6973d2196c
caps.latest.revision: "6"
author: HeidiSteen
ms.author: heidist
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a8a94cb71ab8625a2a546e62f5dc828b605aeaa2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="dax-properties"></a>DAX 属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Msmdsrv.ini 的 DAX 部分包含用于控制中的某些查询行为的设置[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，例如 DAX 查询结果集中返回的行数的上限。 
  
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
