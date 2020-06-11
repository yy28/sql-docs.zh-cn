---
title: 插件算法 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- third-party algorithms [Analysis Services]
- algorithms [data mining], creating
- plugin algorithms [Analysis Services]
ms.assetid: fe364ddc-576e-42fc-9ced-baa399992f92
author: minewiskan
ms.author: owend
ms.openlocfilehash: 69a7f27629025974b0cffcf5c031a861b8e41fa7
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84520914"
---
# <a name="plugin-algorithms"></a>插件算法
  除了提供的算法以外 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，还可以使用其他许多算法进行数据挖掘。 相应地， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 为由第三方创建的“插件”算法提供了某种机制。 只要这些算法遵守特定的标准，就可以像使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 算法一样在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 中使用它们。 插件算法具有提供的算法的所有功能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。  
  
 有关 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 用于与插件算法进行通信的接口的完整说明，请参阅 [CodePlex](https://go.microsoft.com/fwlink/?LinkID=87843) 网站上发布的创建自定义算法和自定义模型查看器的示例。  
  
## <a name="algorithm-requirements"></a>算法要求  
 若要将某个算法插入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，必须实现下列 COM 接口：  
  
 `IDMAlgorithm`  
 实现一个生成模型的算法，并且实现该结果模型的预测操作。  
  
 `IDMAlgorithmNavigation`  
 启用浏览器来访问模型的内容。  
  
 `IDMPersist`  
 启用算法定型，将由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]保存和加载的模型。  
  
 `IDMAlgorithmMetadata`  
 介绍算法的功能和输入参数。  
  
 `IDMAlgorithmFactory`  
 创建实现算法接口的对象的实例，并向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供对算法元数据接口的访问。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用这些 COM 接口与插件算法进行通信。 虽然使用的插件算法必须支持 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB for Data Mining 规范，但是这些算法不必支持该规范中的所有数据挖掘选项。 可以使用 [MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset) 架构行集来确定一个算法的功能。 此架构行集列出了每个插件算法提供程序的数据挖掘支持选项。  
  
 将新算法与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]一起使用之前必须对新算法进行注册。 若要注册一个算法，请将以下信息包含在要将算法包含在其中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的 .ini 文件中：  
  
-   算法名称  
  
-   ProgID（可选并且只能为插件算法包括此信息）  
  
-   指示算法是否启用的标志  
  
 下面的代码示例阐明了如何注册新算法：  
  
 `<ConfigurationSettings>`  
  
 `...`  
  
 `<DataMining>`  
  
 `...`  
  
 `<Algorithms>`  
  
 `...`  
  
 `<Sample_Plugin_Algorithm>`  
  
 `<Enabled>1</Enabled>`  
  
 `<ProgID>Microsoft.DataMining.SamplePlugInAlgorithm.Factory</ProgID>`  
  
 `</Sample_PlugIn_Algorithm>`  
  
 `...`  
  
 `</Algorithms>`  
  
 `...`  
  
 `</DataMining>`  
  
 `...`  
  
 `</ConfigurationSettings>`  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [DMSCHEMA_MINING_SERVICES 行集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset)  
  
  
