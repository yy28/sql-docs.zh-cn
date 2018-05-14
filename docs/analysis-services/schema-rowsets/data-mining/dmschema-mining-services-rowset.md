---
title: DMSCHEMA_MINING_SERVICES 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0cf94fa4fb22e38ac52513d2dba52500df3bb9d5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="dmschemaminingservices-rowset"></a>DMSCHEMA_MINING_SERVICES 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  提供对访问接口支持的每个数据挖掘算法的说明。  
  
## <a name="rowset-columns"></a>行集列  
 **DMSCHEMA_MINING_SERVICES**行集包含以下各列。  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|算法的名称。 此列是特定于访问接口的。|  
|**SERVICE_TYPE_ID**|**DBTYPE_UI4**|此列包含了用于介绍挖掘服务的位图。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 填充此列使用以下值之一：<br /><br /> **DM_SERVICETYPE_CLASSIFICATION** (**1**)<br /><br /> **DM_SERVICETYPE_CLUSTERING** (**2**)|  
|**SERVICE_DISPLAY_NAME**|**DBTYPE_WSTR**|算法的可本地化显示名称。|  
|**SERVICE_GUID**|**DBTYPE_GUID**|算法的 GUID。|  
|**DESCRIPTION**|**DBTYPE_WSTR**|算法的用户友好说明。|  
|**PREDICTION_LIMIT**|**DBTYPE_UI4**|模型和算法可提供的最大预测数。|  
|**SUPPORTED_DISTRIBUTION_FLAGS**|**DBTYPE_WSTR**|描述算法支持的统计分布情况的逗号分隔标志列表。 此列包含一个或多个下列值：<br /><br /> "**正常**"<br /><br /> "**日志正常**"<br /><br /> "**统一**"|  
|**SUPPORTED_INPUT_CONTENT_TYPES**|**DBTYPE_WSTR**|描述算法支持的输入内容类型的逗号分隔标志列表。 此列包含一个或多个下列值：<br /><br /> "**密钥**"<br /><br /> "**离散**"<br /><br /> "**连续**"<br /><br /> "**DISCRETIZED**"<br /><br /> "**ORDERED**"<br /><br /> "密钥**序列**"<br /><br /> "**CYCLICAL**"<br /><br /> "**概率**"<br /><br /> "**方差**"<br /><br /> "**STDEV**"<br /><br /> "**支持**"<br /><br /> "**概率方差**"<br /><br /> "**概率 STDEV**"<br /><br /> "**KEY TIME**"|  
|**SUPPORTED_PREDICTION_CONTENT_TYPES**|**DBTYPE_WSTR**|描述算法支持的预测内容类型的逗号分隔标志列表。 此列包含一个或多个下列值：<br /><br /> "**密钥**"<br /><br /> "**离散**"<br /><br /> "**连续**"<br /><br /> "**DISCRETIZED**"<br /><br /> "**ORDERED**"<br /><br /> "密钥**序列**"<br /><br /> "**CYCLICAL**"<br /><br /> "**概率**"<br /><br /> "**方差**"<br /><br /> "**STDEV**"<br /><br /> "**支持**"<br /><br /> "**概率方差**"<br /><br /> "**概率 STDEV**"<br /><br /> "KEY TIME"|  
|**SUPPORTED_MODELING_FLAGS**|**DBTYPE_WSTR**|算法支持的建模标志的逗号分隔列表。 此列包含一个或多个下列值：<br /><br /> "**MODEL_EXISTENCE_ONLY**"<br /><br /> "**回归量**"<br /><br /> <br /><br /> 请注意也可定义提供程序特定的标志。|  
|**SUPPORTED_SOURCE_QUERY**|**DBTYPE_WSTR**|支持此列以提供向后兼容。|  
|**TRAINING_COMPLEXITY**|**DBTYPE_I4**|预计定型所需的时间：<br /><br /> **DM_TRAINING_COMPLEXITY_LOW**指示正在运行的时间是相对较短，并且它是成比例输入。<br /><br /> **DM_TRAINING_COMPLEXITY_MEDIUM**指示，运行时间可能较长，但通常成比例输入。<br /><br /> **DM_TRAINING_COMPLEXITY_HIGH**指示的运行时间长，并且它可能呈指数级增长关系中的定型事例总数。|  
|**PREDICTION_COMPLEXITY**|**DBTYPE_I4**|预计预测所需的时间：<br /><br /> **DM_PREDICTION_COMPLEXITY_LOW**指示正在运行的时间是相对较短，并且它是成比例输入。<br /><br /> **DM_PREDICTION_COMPLEXITY_MEDIUM**指示，运行时间可能较长，但通常成比例输入。<br /><br /> **DM_PREDICTION_COMPLEXITY_HIGH**指示的运行时间长，并且它可能呈指数级增长关系中的定型事例总数。|  
|**EXPECTED_QUALITY**|**DBTYPE_I4**|使用此算法生成的模型的预期质量：<br /><br /> **DM_EXPECTED_QUALITY_LOW**<br /><br /> **DM_EXPECTED_QUALITY_MEDIUM**<br /><br /> **DM_EXPECTED_QUALITY_HIGH**|  
|**缩放**|**DBTYPE_I4**|算法的可扩展性：<br /><br /> **DM_SCALING_LOW**<br /><br /> **DM_SCALING_MEDIUM**<br /><br /> **DM_SCALING_HIGH**|  
|**ALLOW_INCREMENTAL_INSERT**|**DBTYPE_BOOL**|指示算法是否支持增量定型（即，基于新的事实数据更新已发现的模式，而不是完全重新发现这些模式）的布尔值。|  
|**ALLOW_PMML_INITIALIZATION**|**DBTYPE_BOOL**|指示是否可以基于 PMML 2.1 字符串创建挖掘模型的布尔值。<br /><br /> 如果**TRUE**，挖掘算法支持从 PMML 2.1 内容的初始化。|  
|**控件**|**DBTYPE_I4**|定型中断时，服务提供的支持：<br /><br /> **DM_CONTROL_NONE**指示它启动训练该模型后，无法取消该算法。<br /><br /> **DM_CONTROL_CANCEL**指示它开始训练该模型，但必须重新启动继续训练后，可以取消该算法。<br /><br /> **DM_CONTROL_SUSPENDRESUME**指示算法可以取消，并在任何时候继续，但结果不可用，直到完成培训。<br /><br /> **DM_CONTROL_SUSPENDWITHRESULT**表示算法可以取消，并在任何时候继续，可以获得任何增量结果。|  
|**ALLOW_DUPLICATE_KEY**|**DBTYPE_BOOL**|指示事例中是否可包含重复键的布尔值。<br /><br /> 如果**VARIANT_TRUE**，允许用例包含重复键。|  
|**VIEWER_TYPE**|**DBTYPE_WSTR**|建议用于此模型的查看器。|  
|**HELP_FILE**|**DBTYPE_WSTR**|（可选）包含此服务的文档的文件名。|  
|**HELP_CONTEXT**|**DBTYPE_I4**|（可选）此服务的帮助上下文 ID。|  
|**MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL**|**DBTYPE_WSTR**|支持的 DDL 版本。 0 指示无 DDL 支持。|  
|**MSOLAP_SUPPORTS_OLAP_MINING_MODELS**|**DBTYPE_BOOL**|指示是否可以创建 OLAP 挖掘模型的布尔值。<br /><br /> 如果**TRUE**，可以创建 OLAP 挖掘模型。 需要**MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL**为非零。|  
|**MSOLAP_SUPPORTS_DATA_MINING_DIMENSIONS**|**DBTYPE_BOOL**|指示是否可以创建数据挖掘维度的布尔值。<br /><br /> 如果**TRUE**，可以创建数据挖掘维度。|  
|**MSOLAP_SUPPORTS_DRILLTHROUGH**|**DBTYPE_BOOL**|指示服务是否支持钻取功能的布尔值。<br /><br /> 如果**TRUE**，该服务支持钻取功能。|  
  
## <a name="restriction-columns"></a>限制列  
 **DMSCHEMA_MINING_SERVICES**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SERVICE_TYPE_ID**|**DBTYPE_UI4**|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘架构行集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
