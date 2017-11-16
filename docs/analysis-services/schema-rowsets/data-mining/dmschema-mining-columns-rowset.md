---
title: "DMSCHEMA_MINING_COLUMNS 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_COLUMNS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_COLUMNS rowset
ms.assetid: ae35ccde-4438-46f4-8611-40b2b1a42fce
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aa9ee7c66193eb84f883ba0500a8617421f2228e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingcolumns-rowset"></a>DMSCHEMA_MINING_COLUMNS 行集
  描述中的所有数据挖掘模型的各个列[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 此行集只限于当前目录。  
  
## <a name="rowset-columns"></a>行集列  
 **DMSCHEMA_MINING_COLUMNS**行集包含以下各列。  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|目录名称。 使用模型为其成员的数据库的名称填充。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|非限定的架构名称。 此列不支持通过[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**MODEL_NAME**|**DBTYPE_WSTR**|挖掘模型名称。 此列包含与某列关联的挖掘模型的名称，并且永远不为空。|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|列的名称。|  
|**COLUMN_GUID**|**DBTYPE_GUID**|列 GUID。 此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**COLUMN_PROPID**|**DBTYPE_UI4**|列属性 ID。 此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**|列的序号位置。 列从 1 开始编号。 此列包含**NULL**如果没有稳定序号值的列。|  
|**COLUMN_HAS_DEFAULT**|**DBTYPE_BOOL**|一个布尔值，该值指示列是否具有默认值。<br /><br /> **TRUE**如果列具有默认值，否则**FALSE**。|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**|列的默认值。<br /><br /> 如果默认值是**NULL**值， **COLUMN_HASDEFAULT**包含**TRUE**，并且此列包含**NULL**。|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**|描述特征列的位掩码。 **DBCOLUMNFLAGS**枚举的类型的位掩码中指定的位。 此列永远不为空。|  
|**IS_NULLABLE**|**DBTYPE_BOOL**|指示列是否可以为 Null 的布尔值。<br /><br /> **FALSE**如果列已知不可以为 null; 否则为**TRUE**。|  
|**DATA_TYPE**|**DBTYPE_UI2**|列的数据类型的指示符。 以下列表显示了返回的指示符类型的示例：<br /><br /> "**表**"将返回**DBTYPE_HCHAPTER**。<br /><br /> "**文本**"将返回**DBTYPE_WCHAR**。<br /><br /> "**长**"将返回**是 DBTYPE_I8**。<br /><br /> "**DOUBLE**"将返回**DBTYPE_R8**。<br /><br /> "**日期**"将返回**DBTYPE_DATE**。|  
|**TYPE_GUID**|**DBTYPE_GUID**|列的数据类型的 GUID。 此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**VT_NULL**。|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**|列中值的最大可能长度。 对于字符列、二进制值列或位列，可以是下列值之一：<br /><br /> 如果已定义列的长度，则为字符、字节或位列各自列类型的最大长度。 例如， **CHAR(5)** SQL 表中的列具有的最大长度为 5。<br /><br /> 中的字符、 字节或 bits，如果列不具有定义的长度为列类型中，相应的数据类型最大长度。<br /><br /> 如果列和数据类型的最大长度均未定义，则为零 (0)。<br /><br /> **NULL**对于所有其他类型的列|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**|如果列的类型为字符或二进制值时，则为列的八进制最大长度（字节）。 零值 (0) 表示列没有最大长度。 此列包含**NULL**对于所有其他类型的列。|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**|如果列的数据类型而不是数值数据类型的列的最大精度**VARNUMERIC**。<br /><br /> **NULL**如果列的数据类型不是数值或是**VARNUMERIC**。<br /><br /> 数据类型的列的精度**DBTYPE_DECIMAL**或**DBTYPE_NUMERIC**取决于列定义。|  
|**NUMERIC_SCALE**|**DBTYPE_I2**|如果列的类型指示符为小数点右侧的数字个数**DBTYPE_DECIMAL**， **DBTYPE_NUMERIC**，或**DBTYPE_VARNUMERIC**。 否则，此列将包含**VT_NULL**。|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**|如果列数据类型是日期时间或间隔类型; 列的日期/时间精度 （数秒的小数部分部分中的位数）否则为**NULL**。|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**|在其中定义字符集的目录名称。 此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**|在其中定义字符集的非限定架构名称。 此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**|字符集名称。 此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**|在其中定义排序规则的目录名称。 此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**|在其中定义排序规则架构的非限定的名称。 此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**COLLATION_NAME**|**DBTYPE_WSTR**|排序规则名称。 此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**|在其中定义域的目录名称。 此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**|在其中定义域的非限定架构名称。 此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**A I N _**|**DBTYPE_WSTR**|域名。 此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**DESCRIPTION**|**DBTYPE_WSTR**|列的用户友好的说明此列不支持通过[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**DISTRIBUTION_FLAG**|**DBTYPE_WSTR**|列的统计分布情况的说明。 此列包含以下内容之一：<br /><br /> "**正常**"<br /><br /> "**LOG_NORMAL**"<br /><br /> "**统一**"|  
|**P E**|**DBTYPE_WSTR**|列的内容说明。 此列包含以下内容之一：<br /><br /> "**密钥**"<br /><br /> "**离散**"<br /><br /> "**连续**"<br /><br /> "**DISCRETIZED (**[参数]**)**"<br /><br /> "**ORDERED**"<br /><br /> "**KEY TIME**"<br /><br /> "**CYCLICAL**"<br /><br /> "**概率**"<br /><br /> "**方差**"<br /><br /> "**STDEV**"<br /><br /> "**支持**"<br /><br /> "**PROBABILITY_VARIANCE**"<br /><br /> "**PROBABILITY_STDEV**"<br /><br /> **"KEY SEQUENCE**"|  
|**MODELING_FLAG**|**DBTYPE_WSTR**|逗号分隔的标志列表。 已定义的标志为：<br /><br /> "**MODEL_EXISTENCE_ONLY**"<br /><br /> "**回归量**"<br /><br /> 特定于算法的建模标志也可包含在此列中。|  
|**IS_RELATED_TO_KEY**|**DBTYPE_BOOL**|一个布尔值，该值指示是否与密钥相关列。<br /><br /> **TRUE**如果此列相关的键。 如果键是一个列中， **RELATED_ATTRIBUTE**字段可以根据需要包含的列名称。|  
|**RELATED_ATTRIBUTE**|**DBTYPE_WSTR**|向其当前的列相关，或者特殊属性的目标列的名称。|  
|**IS_INPUT**|**DBTYPE_BOOL**|指示列是否为输入列的布尔值。<br /><br /> **VARIANT_TRUE**如果这是输入的列。|  
|**IS_PREDICTABLE**|**DBTYPE_BOOL**|指示列是否可预测的布尔值。<br /><br /> **TRUE**如果列是可预测。|  
|**CONTAINING_COLUMN**|**DBTYPE_WSTR**|名称**表**包含此列的列。 此列包含**NULL**如果列不包含在另一列。|  
|**PREDICTION_SCALAR_FUNCTIONS**|**DBTYPE_WSTR**|可对列执行的标量函数的逗号分隔列表。|  
|**PREDICTION_TABLE_FUNCTIONS**|**DBTYPE_WSTR**|可应用于该列的函数的逗号分隔列表。 这些函数应返回一个表。 列表的格式如下：<br /><br /> `<function name>(<column1> [, <column2>], ...)`<br /><br /> 此格式允许客户端应用程序确定各函数的签名（参数列表）。|  
|**IS_POPULATED**|**DBTYPE_BOOL**|指示是否已使用一组可能的值为列定型的布尔值。<br /><br /> **TRUE**如果在列训练与一组的可能的值。<br /><br /> 包含**FALSE**如果不填充列。|  
|**PREDICTION_SCORE**|**DBTYPE_R8**|对列进行预测所针对的模型的分数。 分数用于度量模型的准确性。|  
|**SOURCE_COLUMN**|**DBTYPE_WSTR**|当前挖掘列的源挖掘结构列的名称。|  
  
## <a name="restriction-columns"></a>限制列  
 **DMSCHEMA_MINING_COLUMNS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|可选。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|可选。|  
|**MODEL_NAME**|**DBTYPE_WSTR**|可选。|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|可选。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘架构行集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  

