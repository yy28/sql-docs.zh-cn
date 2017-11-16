---
title: "MDSCHEMA_ACTIONS 行集 |Microsoft 文档"
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
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_ACTIONS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_ACTIONS rowset
ms.assetid: f73081f8-ac51-4286-b46e-2b34e792c3e0
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e9abd044460f463b952eb6fbd88cd7d7a4ea2821
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemaactions-rowset"></a>MDSCHEMA_ACTIONS 行集
  介绍可用于客户端应用程序的操作。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_ACTIONS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||数据库的名称。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||不提供支持。 始终包含**VT_NULL**。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||此操作所属的多维数据集的名称。|  
|**ACTION_NAME**|**DBTYPE_WSTR**||此操作的名称。|  
|**ACTION_TYPE**|**DBTYPE_I4**||用于指定相应操作的触发方法的位图。 Msmd.h 文件为此位图定义以下位值常量：<br /><br /> **MDACTION_TYPE_URL** (**0x01**)<br /><br /> **MDACTION_TYPE_HTML** (**0x02**)<br /><br /> **MDACTION_TYPE_STATEMENT** (**0x04，则**)<br /><br /> **MDACTION_TYPE_DATASET** (**0x08**)<br /><br /> **MDACTION_TYPE_ROWSET** (**0x10**)<br /><br /> **MDACTION_TYPE_COMMANDLINE** (**0x20**)<br /><br /> **MDACTION_TYPE_PROPRIETARY** (**0x40**)<br /><br /> **MDACTION_TYPE_REPORT** (**0x80**)<br /><br /> **MDACTION_TYPE_DRILLTHROUGH** (**0x100**)|  
|**坐标**|**DBTYPE_WSTR**||指定相应操作执行时所在的多维空间中的对象或坐标的多维表达式 (MDX) 表达式。 客户端应用程序负责提供此限制列的值。<br /><br /> **CORDINATE**必须解析为中指定的对象**COORDINATE_TYPE**。|  
|**COORDINATE_TYPE**|**DBTYPE_I4**||指定位图如何**协调**解释限制列。 Msmd.h 文件为此位图定义以下位值常量：<br /><br /> **MDACTION_COORDINATE_CUBE** (**1**)<br /><br /> **MDACTION_COORDINATE_DIMENSION** (**2**): 引用的维度层次结构。<br /><br /> **MDACTION_COORDINATE_LEVEL** (**3**)<br /><br /> **MDACTION_COORDINATE_MEMBER** (**4**)<br /><br /> **MDACTION_COORDINATE_SET** (**5**)<br /><br /> **MDACTION_COORDINATE_CELL** (**6**)|  
|**ACTION_CAPTION**|**DBTYPE_WSTR**||如果未指定标题并且未在 DDL 中指定翻译，则为相应的操作名称。<br /><br /> 如果指定一个标题或翻译，和**CaptionIsMDX**为 false，以下字符串之一：<br /><br /> 的适当的语言转换。<br /><br /> 如果不进行转换找到指定的语言-指定的标题。<br /><br /> 的如果找不进行转换操作名称，并将标题 DDL 中未指定。<br /><br /> 如果指定一个标题或翻译，和**CaptionIsMDX**为 true，导致对指定的语言或在 DDL 标题中，指定的平移查找适当的翻译和计算的字符串若要创建字符串的公式。<br /><br /> 如果相应操作已在 MDX 脚本中指定，则不会有翻译，且标题始终被视为 MDX 表达式。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||操作的用户友好说明。|  
|**内容**|**DBTYPE_WSTR**||将要运行的操作的表达式或内容。|  
|**应用程序**|**DBTYPE_WSTR**||将用于运行相应操作的应用程序的名称。|  
|**调用**|**DBTYPE_I4**||与应如何调用相应操作有关的信息：<br /><br /> **MDACTION_INVOCATION_INTERACTIVE** (**1**) 指示在正常操作过程中使用的常规操作。 这是此列的默认值。<br /><br /> **MDACTION_INVOCATION_ON_OPEN** (**2**) 指示首次打开多维数据集时，应执行的操作。<br /><br /> **MDACTION_INVOCATION_BATCH** (**4**) 指示操作执行批处理操作的一部分或[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]任务。<br /><br /> <br /><br /> 请注意，在文件中，Msmd.h 定义这些枚举值。|  
  
 行集按排序**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**， **ACTION_NAME**。  
  
> [!NOTE]  
>  操作的**MDACTION_TYPE_PROPRIETARY**类型必须提供一个值**应用程序**列。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_ACTIONS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|可选|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|可选|  
|**CUBE_NAME**|**DBTYPE_WSTR**|必需|  
|**ACTION_NAME**|**DBTYPE_WSTR**|可选|  
|**ACTION_TYPE**|**DBTYPE_I4**|可选|  
|**坐标**|**DBTYPE_WSTR**|必需|  
|**COORDINATE_TYPE**|**DBTYPE_I4**|必需|  
|**调用**|**DBTYPE_I4**|（可选）**调用**限制列默认值为**MDACTION_INVOCATION_INTERACTIVE**。 若要检索的所有操作，请使用**MDACTION_INVOCATION_ALL**中的值**调用**限制列。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用以下有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
  
> [!IMPORTANT]  
>  **调用**限制列具有默认值为**MDACTION_INVOCATION_INTERACTIVE**。 任何未为该列显式指定值的架构行集仅包含具有该值的行。 如果你想要包含操作的整个集的行集，使用**MDACTION_INVOCATION_ALL**常量中**调用**限制列。  
  
 客户端应用程序可以定义多个**ACTION_TYPE**使用 OR 运算符。  
  
## <a name="remarks"></a>注释  
 下表列出了有效**协调**和**COORDINATE_TYPE**组合。  
  
|COORDINATE 对象类型|COORDINATE_TYPE|  
|----------------------------|----------------------|  
|**Cube**|**MDACTION_COORDINATE_CUBE**|  
|**Dimension**|**MDACTION_COORDINATE_DIMENSION**<br /><br /> **MDACTION_COORDINATE_LEVEL**<br /><br /> **MDACTION_COORDINATE_MEMBER**<br /><br /> **MDACTION_COORDINATE_SET**<br /><br /> **MDACTION_COORDINATE_CELL**|  
|**Hierarchy**|**MDACTION_COORDINATE_DIMENSION**|  
|**Level**|**MDACTION_COORDINATE_LEVEL**|  
|**成员**|**MDACTION_COORDINATE_MEMBER**|  
|**设置**|**MDACTION_COORDINATE_SET**|  
|**单元格**|**MDACTION_COORDINATE_CELL**|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

