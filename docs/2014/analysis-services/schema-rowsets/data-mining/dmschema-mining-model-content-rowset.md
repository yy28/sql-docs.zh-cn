---
title: DMSCHEMA_MINING_MODEL_CONTENT 行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DMSCHEMA_MINING_MODEL_CONTENT
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_CONTENT rowset
ms.assetid: 1e85d9e7-3b74-42ac-b94e-f52f76d8a25d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e23e78bd3588dd31a11c39941572645fb11771d1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172277"
---
# <a name="dmschemaminingmodelcontent-rowset"></a>DMSCHEMA_MINING_MODEL_CONTENT 行集
  允许客户端应用程序浏览数据挖掘模型的内容。 客户端应用程序可使用本主题结尾处介绍的特殊树操作限制来浏览挖掘模型的内容。  
  
## <a name="rowset-columns"></a>行集列  
 `DMSCHEMA_MINING_MODEL_CONTENT`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||目录名称。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用填充此列的模型成员的数据库名称。|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||非限定的架构名称。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `VT_NULL`。|  
|`MODEL_NAME`|`DBTYPE_WSTR`||与此行描述的内容关联的模型的名称。|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||与此节点对应的属性的名称。|  
|`NODE_NAME`|`DBTYPE_WSTR`||节点的名称。 目前，此列包含的值与 `NODE_UNIQUE_NAME` 的值相同，但是这一情况在以后的版本中可能会发生变化。|  
|`NODE_UNIQUE_NAME`|`DBTYPE_WSTR`||节点的唯一名称。|  
|`NODE_TYPE`|`DBTYPE_I4`||节点的类型。 将会生成下列值之一（第三方数据挖掘算法可扩展此列表）：<br /><br /> -   `DM_NODE_TYPE_CLASSIFICATION_TREE_ROOT` (`2`)<br />-   `DM_NODE_TYPE_TREE_INTERIOR` (`3`)<br />-   `DM_NODE_TYPE_TREE_DISTRIBUTION` (`4`)<br />-   `DM_NODE_TYPE_CLUSTER` (`5`)<br />-   `DM_NODE_TYPE_UNKNOWN` (`6`)<br />-   `DM_NODE_TYPE_ITEMSET` (`7`)<br />-   `DM_NODE_TYPE_ASSOCIATION_RULE` (`8`)<br />-   `DM_NODE_TYPE_NB_PREDICTABLE_ATTRIBUTE` (`9`)<br />-   `DM_NODE_TYPE_NB_INPUT_ATTRIBUTE` (`10`)<br />-   `DM_NODE_TYPE_NB_INPUT_ATTRIBUTE_STATE` (`11`)<br />-   `DM_NODE_TYPE_SEQUENCE` (`13`)<br />-   `DM_NODE_TYPE_TRANSITION` (`14`)<br />-   `DM_NODE_TYPE_TIME_SERIES` (`15`)<br />-   `DM_NODE_TYPE_TS_TREE` (`16`)<br />-   `DM_NODE_TYPE_NN_SUBNETWORK` (`17`) 神经网络、 子网<br />-   `DM_NODE_TYPE_NN_INPUT_LAYER` (`18`) 神经网络，输入层 （输入节点的父级）<br />-   **DM_NODE_TYPE_NN_HIDDEN_LAYER** (`19`) 神经网络，隐藏层 （隐藏节点的父级）<br />-   `DM_NODE_TYPE_NN_OUTPUT_LAYER` (`20`) 神经网络，输出层 （输出节点的父级）<br />-   `DM_NODE_TYPE_NN_INPUT_NODE` (`21`) 神经网络，输入的节点<br />-   `DM_NODE_TYPE_NN_HIDDEN_NODE` (`22`) 神经网络，隐藏的节点<br />-   `DM_NODE_TYPE_NN_OUTPUT_NODE` (`23`) 神经网络，输出节点<br />-   `DM_NODE_TYPE_NN_MARGINAL_STAT_NODE` (`24`) 神经网络，边际统计信息节点<br />-   **DM_NODE_TYPE_REGRESSION_TREE_ROOT** (`25`)<br />-   `DM_NODE_TYPE_NB_MARGINAL_STAT_NODE` (`26`) 神经网络，边际统计信息节点|  
|`NODE_GUID`|`DBTYPE_GUID`||节点 GUID。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`NODE_CAPTION`|`DBTYPE_WSTR`||与节点关联的标签或标题。 此属性主要用于显示目的。|  
|`CHILDREN_CARDINALITY`|`DBTYPE_UI4`||对节点所具有的子节点数的估计。|  
|`PARENT_UNIQUE_NAME`|`DBTYPE_WSTR`||节点的父节点的唯一名称。 根级别上的任何节点均返回 `NULL`。|  
|`NODE_DESCRIPTION`|`DBTYPE_WSTR`||节点的用户友好说明。|  
|`NODE_RULE`|`DBTYPE_WSTR`||嵌入节点的规则的 XML 说明。|  
|`MARGINAL_RULE`|`DBTYPE_WSTR`||从父节点移至该节点的规则的 XML 说明。|  
|`NODE_PROBABILITY`|`DBTYPE_R8`||与此节点相关联的概率。|  
|`MARGINAL_PROBABILITY`|`DBTYPE_R8`||从父节点到达该节点的概率。|  
|`NODE_DISTRIBUTION`|`DBTYPE_HCHAPTER`||包含节点的概率直方图的表。|  
|`NODE_SUPPORT`|`DBTYPE_R8`||支持此节点的事例的数目。|  
|`MSOLAP_MODEL_COLUMN`|`DBTYPE_WSTR`||与此节点相关的模型定义中的列名。|  
|`MSOLAP_NODE_SCORE`|`DBTYPE_R8`||针对此节点计算的分数。|  
|`MSOLAP_NODE_SHORT_CAPTION`|`DBTYPE_WSTR`||可用于显示以提高可读性的节点的短标题。|  
  
## <a name="restriction-columns"></a>限制列  
 `DMSCHEMA_MINING_MODEL_CONTENT`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|可选。|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|可选。|  
|`MODEL_NAME`|`DBTYPE_WSTR`|可选。|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`|可选。|  
|`NODE_NAME`|`DBTYPE_WSTR`|可选。|  
|`NODE_UNIQUE_NAME`|`DBTYPE_WSTR`|可选。|  
|`NODE_TYPE`|`DBTYPE_I4`|可选。|  
|`NODE_GUID`|`DBTYPE_WSTR`|可选。|  
|`NODE_CAPTION`|`DBTYPE_WSTR`|可选。|  
|`TREE_OPERATION`|`DBTYPE_UI4`|可选。 有关其他备注，请参阅下文。|  
  
 `TREE_OPERATION` 限制不针对 `DMSCHEMA_MINING_MODEL_CONTENT` 行集的任何特定列；它指定树运算符。 使用者可以指定 `NODE_UNIQUE_NAME` 限制和树运算符（`ANCESTORS`、`CHILDREN`、`SIBLINGS`、`PARENT`、`DESCENDANTS`、`SELF`）来获取请求的成员集。 `SELF` 运算符包含返回行列表中节点本身所在的行。 下表介绍了组成 `TREE_OPERATION` 限制的位图定义的常量。 可以使用逻辑 `OR` 运算符组合这些常量。  
  
|常量|ReplTest1|  
|--------------|-----------|  
|**DMTREEOP_ANCESTORS**|`0x00000020`|  
|**DMTREEOP_CHILDREN**|`0x00000001`|  
|**DMTREEOP_SIBLINGS**|`0x00000002`|  
|**DMTREEOP_PARENT**|`0x00000004`|  
|**DMTREEOP_SELF**|`0x00000008`|  
|**DMTREEOP_DESCENDANTS**|`0x00000010`|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘架构行集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
