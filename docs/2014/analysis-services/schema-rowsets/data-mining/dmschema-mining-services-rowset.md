---
title: DMSCHEMA_MINING_SERVICES 行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DMSCHEMA_MINING_SERVICES
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICES rowset
ms.assetid: 4a672f2f-d637-4def-a572-c18556f83d34
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e6ccfdba24d7bc23b97eb15e61321f82e5ab1d9b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278210"
---
# <a name="dmschemaminingservices-rowset"></a>DMSCHEMA_MINING_SERVICES 行集
  提供对访问接口支持的每个数据挖掘算法的说明。  
  
## <a name="rowset-columns"></a>行集列  
 `DMSCHEMA_MINING_SERVICES`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||算法的名称。 此列是特定于访问接口的。|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`||此列包含了用于介绍挖掘服务的位图。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用填充此列使用以下值之一：<br /><br /> -   `DM_SERVICETYPE_CLASSIFICATION` (`1`)<br />-   `DM_SERVICETYPE_CLUSTERING` (`2`)|  
|`SERVICE_DISPLAY_NAME`|`DBTYPE_WSTR`||算法的可本地化显示名称。|  
|`SERVICE_GUID`|`DBTYPE_GUID`||算法的 GUID。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||算法的用户友好说明。|  
|`PREDICTION_LIMIT`|`DBTYPE_UI4`||模型和算法可提供的最大预测数。|  
|`SUPPORTED_DISTRIBUTION_FLAGS`|`DBTYPE_WSTR`||描述算法支持的统计分布情况的逗号分隔标志列表。 此列包含一个或多个下列值：<br /><br /> -   "`NORMAL`"<br />-   "`LOG NORMAL`"<br />-   "`UNIFORM`"|  
|`SUPPORTED_INPUT_CONTENT_TYPES`|`DBTYPE_WSTR`||描述算法支持的输入内容类型的逗号分隔标志列表。 此列包含一个或多个下列值：<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-   "`DISCRETIZED`"<br />-   "`ORDERED`"<br />-"键`SEQUENCE`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY VARIANCE`"<br />-   "`PROBABILITY STDEV`"<br />-   "`KEY TIME`"|  
|`SUPPORTED_PREDICTION_CONTENT_TYPES`|`DBTYPE_WSTR`||描述算法支持的预测内容类型的逗号分隔标志列表。 此列包含一个或多个下列值：<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-   "`DISCRETIZED`"<br />-   "`ORDERED`"<br />-"键`SEQUENCE`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY VARIANCE`"<br />-   "`PROBABILITY STDEV`"<br />-"键时间"|  
|`SUPPORTED_MODELING_FLAGS`|`DBTYPE_WSTR`||算法支持的建模标志的逗号分隔列表。 此列包含一个或多个下列值：<br /><br /> -   "`MODEL_EXISTENCE_ONLY`"<br />-   "`REGRESSOR`"<br /><br /> 还可定义特定于访问接口的标志。|  
|`SUPPORTED_SOURCE_QUERY`|`DBTYPE_WSTR`||-为了向后兼容支持此列。|  
|`TRAINING_COMPLEXITY`|`DBTYPE_I4`||预计定型所需的时间：<br /><br /> -   `DM_TRAINING_COMPLEXITY_LOW` 指示运行时间是相对较短，并且它是与输入成比例。<br />-   **DM_TRAINING_COMPLEXITY_MEDIUM**指示运行时间可能较长，但它是通常与输入成比例。<br />-   **DM_TRAINING_COMPLEXITY_HIGH**指示运行时间长，并且它可能会呈指数级增长关系中到定型事例的数目。|  
|`PREDICTION_COMPLEXITY`|`DBTYPE_I4`||预计预测所需的时间：<br /><br /> -   **DM_PREDICTION_COMPLEXITY_LOW**指示运行时间是相对较短，并且它是与输入成比例。<br />-   **DM_PREDICTION_COMPLEXITY_MEDIUM**指示运行时间可能较长，但它是通常与输入成比例。<br />-   **DM_PREDICTION_COMPLEXITY_HIGH**指示运行时间长，并且它可能会呈指数级增长关系中到定型事例的数目。|  
|`EXPECTED_QUALITY`|`DBTYPE_I4`||使用此算法生成的模型的预期质量：<br /><br /> -   `DM_EXPECTED_QUALITY_LOW`<br />-   `DM_EXPECTED_QUALITY_MEDIUM`<br />-   **DM_EXPECTED_QUALITY_HIGH**|  
|`SCALING`|`DBTYPE_I4`||算法的可扩展性：<br /><br /> -   **DM_SCALING_LOW**<br />-   `DM_SCALING_MEDIUM`<br />-   **DM_SCALING_HIGH**|  
|`ALLOW_INCREMENTAL_INSERT`|`DBTYPE_BOOL`||指示算法是否支持增量定型（即，基于新的事实数据更新已发现的模式，而不是完全重新发现这些模式）的布尔值。|  
|`ALLOW_PMML_INITIALIZATION`|`DBTYPE_BOOL`||指示是否可以基于 PMML 2.1 字符串创建挖掘模型的布尔值。<br /><br /> 如果为 `TRUE`，则挖掘算法支持从 PMML 2.1 内容进行初始化。|  
|`CONTROL`|`DBTYPE_I4`||定型中断时，服务提供的支持：<br /><br /> -   `DM_CONTROL_NONE` 指示在启动来训练模型后不能取消算法。<br />-   `DM_CONTROL_CANCEL` 指示它开始为定型模型，但必须重新启动要恢复定型后，可以取消算法。<br />-   `DM_CONTROL_SUSPENDRESUME` 指示算法可以取消和恢复在任何时候，但结果不可用，直到完成培训后。<br />-   `DM_CONTROL_SUSPENDWITHRESULT` 指示算法可以取消和恢复在任何时候，并且可以获取任何增量结果。|  
|`ALLOW_DUPLICATE_KEY`|`DBTYPE_BOOL`||指示事例中是否可包含重复键的布尔值。<br /><br /> 如果为 `VARIANT_TRUE`，则允许事例包含重复键。|  
|`VIEWER_TYPE`|`DBTYPE_WSTR`||建议用于此模型的查看器。|  
|`HELP_FILE`|`DBTYPE_WSTR`||（可选）包含此服务的文档的文件名。|  
|`HELP_CONTEXT`|`DBTYPE_I4`||（可选）此服务的帮助上下文 ID。|  
|`MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL`|`DBTYPE_WSTR`||支持的 DDL 版本。 0 指示无 DDL 支持。|  
|`MSOLAP_SUPPORTS_OLAP_MINING_MODELS`|`DBTYPE_BOOL`||指示是否可以创建 OLAP 挖掘模型的布尔值。<br /><br /> 如果为 `TRUE`，则可以创建 OLAP 挖掘模型。 要求 `MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL` 非零。|  
|`MSOLAP_SUPPORTS_DATA_MINING_DIMENSIONS`|`DBTYPE_BOOL`||指示是否可以创建数据挖掘维度的布尔值。<br /><br /> 如果为 `TRUE`，则可以创建数据挖掘维度。|  
|`MSOLAP_SUPPORTS_DRILLTHROUGH`|`DBTYPE_BOOL`||指示服务是否支持钻取功能的布尔值。<br /><br /> 如果为 `TRUE`，则服务支持钻取功能。|  
  
## <a name="restriction-columns"></a>限制列  
 `DMSCHEMA_MINING_SERVICES`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|可选。|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`|可选。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘架构行集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
