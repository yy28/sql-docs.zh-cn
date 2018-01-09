---
title: "StorageEngineUsed 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: StorageEngineUsed Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
ms.assetid: 98895c10-f3c2-4d8a-be94-6128c828561d
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bbd6a47e68c069ca9eef8c8fe8f414d4025ebeba
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="storageengineused-element-xmla"></a>StorageEngineUsed 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含一个只读的值，描述当前的数据库类型。  
  
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
            <StorageEngineUsed >...</StorageEngineUsed>  
   </Database>  
</Databases>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[database](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*传统*|数据库模型对应于 MOLAP、ROLAP 或 HOLAP 存储模式。|  
|*InMemory*|数据库模型对应于 IMBI 存储模式。|  
|*混合*|数据库模型将 IMBI 与 MOLAP、ROLAP 或 HOLAP 存储模式混合在一起。|  
  
 对应于的允许值为枚举**StorageEngineUsed**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.StorageEngineUsed>。  
  
 对应的父级的元素**StorageEngineUsed**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.Database>。  
  
  
