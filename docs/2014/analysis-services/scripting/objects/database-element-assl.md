---
title: 数据库元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Database Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DATABASE
helpviewer_keywords:
- Database element
ms.assetid: c3bc7eaf-ed0d-4395-a3b7-8d9cfacfe911
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 56efc69c0e8f7f0e3e008aa5ea769774ee5014af
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37332813"
---
# <a name="database-element-assl"></a>Database 元素 (ASSL)
  定义[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Databases>  
   <Database>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastUpdate>...</LastUpdate>  
      <Description>...</Description>  
      <State>   </State>  
      <AggregationPrefix>...</AggregationPrefix>  
      <EstimatedSize>...</EstimatedSize>  
      <LastProcessed>...</LastProcessed>  
      <Language>...</Language>  
            <Collation>...</Collation>  
      <Visible>...</Visible>  
      <MasterDatasourceID>...</MasterDataSourceID>  
      <Accounts>...</Accounts>  
      <DataSources>...</DataSources>  
      <DataSourceViews>...</DataSourceViews>  
      <Dimensions>...</Dimensions>  
      <Cubes>...</Cubes>  
      <MiningStructures>...</MiningStructures>  
            <Roles>...</Roles>  
      <Assemblies>...</Assemblies>  
      <DatabasePermissions>...</DatabasePermissions>  
            <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Database>  
</Databases>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[数据库](../collections/databases-element-assl.md)|  
|子元素|[帐户](../collections/accounts-element-assl.md)， [AggregationPrefix](../properties/aggregationprefix-element-assl.md)，[批注](../collections/annotations-element-assl.md)，[程序集](../collections/assemblies-element-assl.md)，[排序规则](../properties/collation-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)，[多维数据集](../collections/cubes-element-assl.md)， [DatabasePermissions](../collections/databasepermissions-element-assl.md)， [DataSources](../collections/datasources-element-assl.md)， [DataSourceViews](../collections/datasourceviews-element-assl.md)，[描述](../properties/description-element-assl.md)，[维度](../collections/dimensions-element-assl.md)， [EstimatedSize](../properties/estimatedsize-element-assl.md)， [ID](../properties/id-element-assl.md)，[语言](../properties/language-element-assl.md)， [LastProcessed](../properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [LastUpdate](../properties/lastupdate-element-assl.md)， [MasterDatasourceID](../properties/datasourceid-element-assl.md)， [MiningStructures](../collections/miningstructures-element-assl.md)，[名称](../properties/name-element-assl.md)，[角色](../collections/roles-element-assl.md)，[状态](../properties/state-element-assl.md)，[翻译](../collections/translations-element-assl.md)，[可见](../properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Database>。  
  
## <a name="see-also"></a>请参阅  
 [服务器元素&#40;ASSL&#41;](server-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
