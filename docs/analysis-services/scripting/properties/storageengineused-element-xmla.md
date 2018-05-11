---
title: StorageEngineUsed 元素 (XMLA) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ab89b65d0b63e36072b6dddbf151ca2af9598276
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="storageengineused-element-xmla"></a>StorageEngineUsed 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含一个说明当前数据库类型的只读值。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[database](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*传统*|数据库模型对应于 MOLAP、ROLAP 或 HOLAP 存储模式。|  
|*InMemory*|数据库模型对应于 IMBI 存储模式。|  
|*混合*|数据库模型将 IMBI 与 MOLAP、ROLAP 或 HOLAP 存储模式混合在一起。|  
  
 对应于的允许值为枚举**StorageEngineUsed**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.StorageEngineUsed>。  
  
 对应的父级的元素**StorageEngineUsed**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.Database>。  
  
  
