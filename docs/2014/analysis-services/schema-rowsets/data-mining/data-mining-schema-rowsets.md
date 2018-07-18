---
title: 数据挖掘架构行集 |Microsoft Docs
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
topic_type:
- apiref
- apinav
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- schema rowsets [Analysis Services]
- rowsets [Analysis Services], data mining
- data mining [Analysis Services], schema rowsets
ms.assetid: bd7d5df5-500b-4159-8467-880e141bc043
caps.latest.revision: 43
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a3b3e54f53eb93ea58a45c92e88503a186a441f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37210047"
---
# <a name="data-mining-schema-rowsets"></a>Data Mining Schema Rowsets
  正在运行的服务器[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支持以下数据挖掘架构行集。 若要检查特定 XML/A 访问接口是否支持特定行集，请使用[DISCOVER_ENUMERATORS](../xml/discover-enumerators-rowset.md)行集与[Discover](../../xmla/xml-elements-methods-discover.md)方法。  
  
 在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中，数据挖掘架构行集在 Transact-SQL 语言中以表的形式在 $SYSTEM 架构中公开。 例如，以下对 Analysis Services 实例的查询返回当前实例上可用的架构列表。  
  
```  
SELECT * FROM [$system].[DBSCHEMA_TABLES]  
```  
  
## <a name="in-this-section"></a>本节内容  
  
|架构行集|Description|  
|-------------------|-----------------|  
|[DMSCHEMA_MINING_COLUMNS 行集](dmschema-mining-columns-rowset.md)|描述在服务器上部署的所有已定义数据挖掘模型的各个列。|  
|[DMSCHEMA_MINING_FUNCTIONS 行集](dmschema-mining-functions-rowset.md)|描述可用于安装在服务器上的每个数据挖掘算法的预测函数和挖掘函数。|  
|[DMSCHEMA_MINING_MODEL_CONTENT 行集](dmschema-mining-model-content-rowset.md)|允许客户端应用程序浏览定型的数据挖掘模型的内容。|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML 行集](dmschema-mining-model-content-pmml-rowset.md)|返回挖掘模型内容的 XML (PMML 2.1) 表示形式。|  
|[DMSCHEMA_MINING_MODEL_XML 行集](dmschema-mining-model-xml-rowset.md)|返回挖掘模型的 XML (PMML 2.1) 结构。 这与 DMSCHEMA_MINING_MODEL_PMML 架构相同，保留此项是为了向后兼容。|  
|[DMSCHEMA_MINING_MODELS 行集](dmschema-mining-models-rowset.md)|枚举在服务器上部署的数据挖掘模型。|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS 行集](dmschema-mining-service-parameters-rowset.md)|提供一个参数列表，这些参数可用于配置安装在服务器上的每个数据挖掘算法的行为。|  
|[DMSCHEMA_MINING_SERVICES 行集](dmschema-mining-services-rowset.md)|提供服务器上可用的每个数据挖掘算法的说明。|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS 行集](dmschema-mining-structure-columns-rowset.md)|描述在服务器上部署的所有挖掘结构的各个列。|  
|[DMSCHEMA_MINING_STRUCTURES 行集](dmschema-mining-structures-rowset.md)|枚举有关挖掘结构的信息。|  
  
 此处列出的所有架构行集都支持的正在运行的服务器[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 架构行集](../../schema-rowsets/analysis-services-schema-rowsets.md)   
 [查询 SQL Server 系统目录](https://technet.microsoft.com/en-us/library/ms189082\(v=sql.110\).aspx)   
 [查询数据挖掘架构行集&#40;Analysis Services-数据挖掘&#41;](../../data-mining/data-mining-schema-rowsets-ssas.md)  
  
  
