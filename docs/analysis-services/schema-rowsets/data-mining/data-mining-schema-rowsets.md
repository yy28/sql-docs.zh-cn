---
title: 数据挖掘架构行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ee1f8d3288d884f7322fa578d8cd9b58919c335b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="data-mining-schema-rowsets"></a>Data Mining Schema Rowsets
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  正在运行的服务器[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支持以下数据挖掘架构行集。 若要检查特定的 XML/A 提供程序是否支持特定的行集，请使用[DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)行集[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法。  
  
 在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中，数据挖掘架构行集在 Transact-SQL 语言中以表的形式在 $SYSTEM 架构中公开。 例如，以下对 Analysis Services 实例的查询返回当前实例上可用的架构列表。  
  
```  
SELECT * FROM [$system].[DBSCHEMA_TABLES]  
```  
  
## <a name="in-this-section"></a>本節內容  
  
|架构行集|Description|  
|-------------------|-----------------|  
|[DMSCHEMA_MINING_COLUMNS 行集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-columns-rowset.md)|描述在服务器上部署的所有已定义数据挖掘模型的各个列。|  
|[DMSCHEMA_MINING_FUNCTIONS 行集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-functions-rowset.md)|描述可用于安装在服务器上的每个数据挖掘算法的预测函数和挖掘函数。|  
|[DMSCHEMA_MINING_MODEL_CONTENT 行集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)|允许客户端应用程序浏览定型的数据挖掘模型的内容。|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML 行集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|返回挖掘模型内容的 XML (PMML 2.1) 表示形式。|  
|[DMSCHEMA_MINING_MODEL_XML 行集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-xml-rowset.md)|返回挖掘模型的 XML (PMML 2.1) 结构。 这与 DMSCHEMA_MINING_MODEL_PMML 架构相同，保留此项是为了向后兼容。|  
|[DMSCHEMA_MINING_MODELS 行集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-models-rowset.md)|枚举在服务器上部署的数据挖掘模型。|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS 行集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)|提供一个参数列表，这些参数可用于配置安装在服务器上的每个数据挖掘算法的行为。|  
|[DMSCHEMA_MINING_SERVICES 行集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)|提供服务器上可用的每个数据挖掘算法的说明。|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS 行集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset.md)|描述在服务器上部署的所有挖掘结构的各个列。|  
|[DMSCHEMA_MINING_STRUCTURES 行集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structures-rowset.md)|枚举有关挖掘结构的信息。|  
  
 正在运行的服务器支持此处列出的所有架构行集[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 架构行集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [数据挖掘架构行集&#40;SSAs&#41;](../../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md)  
  
  
