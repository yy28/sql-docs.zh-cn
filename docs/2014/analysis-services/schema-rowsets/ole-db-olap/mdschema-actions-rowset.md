---
title: MDSCHEMA_ACTIONS 行集 |Microsoft Docs
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
- MDSCHEMA_ACTIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_ACTIONS rowset
ms.assetid: f73081f8-ac51-4286-b46e-2b34e792c3e0
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c7382056922a52e734df61015df85930682d0db0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319367"
---
# <a name="mdschemaactions-rowset"></a>MDSCHEMA_ACTIONS 行集
  介绍可用于客户端应用程序的操作。  
  
## <a name="rowset-columns"></a>行集列  
 `MDSCHEMA_ACTIONS`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||数据库的名称。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不提供支持。 始终包含 `VT_NULL`。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||此操作所属的多维数据集的名称。|  
|`ACTION_NAME`|`DBTYPE_WSTR`||此操作的名称。|  
|`ACTION_TYPE`|`DBTYPE_I4`||用于指定相应操作的触发方法的位图。 Msmd.h 文件为此位图定义以下位值常量：<br /><br /> -   `MDACTION_TYPE_URL` (`0x01`)<br />-   `MDACTION_TYPE_HTML` (`0x02`)<br />-   `MDACTION_TYPE_STATEMENT` (`0x04`)<br />-   `MDACTION_TYPE_DATASET` (`0x08`)<br />-   `MDACTION_TYPE_ROWSET` (`0x10`)<br />-   `MDACTION_TYPE_COMMANDLINE` (`0x20`)<br />-   `MDACTION_TYPE_PROPRIETARY` (`0x40`)<br />-   `MDACTION_TYPE_REPORT` (`0x80`)<br />-   `MDACTION_TYPE_DRILLTHROUGH` (`0x100`)|  
|`COORDINATE`|`DBTYPE_WSTR`||指定相应操作执行时所在的多维空间中的对象或坐标的多维表达式 (MDX) 表达式。 客户端应用程序负责提供此限制列的值。<br /><br /> `CORDINATE` 必须解析为 `COORDINATE_TYPE` 中指定的对象。|  
|`COORDINATE_TYPE`|`DBTYPE_I4`||用于指定 `COORDINATE` 限制列的解释方式的位图。 Msmd.h 文件为此位图定义以下位值常量：<br /><br /> -   `MDACTION_COORDINATE_CUBE` (`1`)<br />-   `MDACTION_COORDINATE_DIMENSION` (`2`)<br />     引用维度层次结构。<br />-   `MDACTION_COORDINATE_LEVEL` (`3`)<br />-   `MDACTION_COORDINATE_MEMBER` (`4`)<br />-   `MDACTION_COORDINATE_SET` (`5`)<br />-   `MDACTION_COORDINATE_CELL` (`6`)|  
|`ACTION_CAPTION`|`DBTYPE_WSTR`||如果未指定标题并且未在 DDL 中指定翻译，则为相应的操作名称。<br /><br /> 如果已指定标题或翻译，且 `CaptionIsMDX` 为 False，则为以下字符串之一：<br /><br /> 的相应的语言翻译。<br />的如果未找到翻译为指定的语言指定的标题。<br />的如果未找到翻译并且未在 DDL 中指定标题操作名称。<br /><br /> 如果已指定标题或翻译，且 `CaptionIsMDX` 为 True，则为通过以下过程得到的字符串：找到指定语言的相应翻译或 DDL 标题中指定的翻译中查找，然后通过计算公式来创建该字符串。<br /><br /> 如果相应操作已在 MDX 脚本中指定，则不会有翻译，且标题始终被视为 MDX 表达式。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||操作的用户友好说明。|  
|`CONTENT`|`DBTYPE_WSTR`||将要运行的操作的表达式或内容。|  
|`APPLICATION`|`DBTYPE_WSTR`||将用于运行相应操作的应用程序的名称。|  
|`INVOCATION`|`DBTYPE_I4`||与应如何调用相应操作有关的信息：<br /><br /> -   `MDACTION_INVOCATION_INTERACTIVE` (`1`) 指示在正常操作过程中使用的常规操作。 这是此列的默认值。<br />-   `MDACTION_INVOCATION_ON_OPEN` (`2`) 指示首次打开多维数据集时应执行的操作。<br />-   `MDACTION_INVOCATION_BATCH` (`4`) 指示批处理操作的一部分执行的操作或[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]任务。<br /><br /> 在文件 Msmd.h 中定义了这些枚举值。|  
  
 行集按 `CATALOG_NAME`、`SCHEMA_NAME`、`CUBE_NAME`、`ACTION_NAME` 排序。  
  
> [!NOTE]  
>  `MDACTION_TYPE_PROPRIETARY` 类型的操作必须为 `APPLICATION` 列提供值。  
  
## <a name="restriction-columns"></a>限制列  
 `MDSCHEMA_ACTIONS`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|可选|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|可选|  
|`CUBE_NAME`|`DBTYPE_WSTR`|必需|  
|`ACTION_NAME`|`DBTYPE_WSTR`|可选|  
|`ACTION_TYPE`|`DBTYPE_I4`|可选|  
|`COORDINATE`|`DBTYPE_WSTR`|必需|  
|`COORDINATE_TYPE`|`DBTYPE_I4`|必需|  
|`INVOCATION`|`DBTYPE_I4`|（可选）`INVOCATION` 限制列的默认值为 `MDACTION_INVOCATION_INTERACTIVE`。 若要检索所有操作，请使用 `MDACTION_INVOCATION_ALL` 限制列中的 `INVOCATION` 值。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|（可选）使用以下有效值之一位图：<br /><br /> -1 的多维数据集<br />-2 个维度<br /><br /> 默认限制的值为 1。|  
  
> [!IMPORTANT]  
>  `INVOCATION` 限制列的默认值为 `MDACTION_INVOCATION_INTERACTIVE`。 任何未为该列显式指定值的架构行集仅包含具有该值的行。 如果希望相应的行集包含整个操作集，请在 `MDACTION_INVOCATION_ALL` 限制列中使用 `INVOCATION` 常量。  
  
 客户端应用程序可通过使用 OR 运算符定义多个 `ACTION_TYPE`。  
  
## <a name="remarks"></a>Remarks  
 下表列出了有效的 `COORDINATE` 和 `COORDINATE_TYPE` 组合。  
  
|COORDINATE 对象类型|COORDINATE_TYPE|  
|----------------------------|----------------------|  
|`Cube`|`MDACTION_COORDINATE_CUBE`|  
|`Dimension`|`MDACTION_COORDINATE_DIMENSION`<br /><br /> `MDACTION_COORDINATE_LEVEL`<br /><br /> `MDACTION_COORDINATE_MEMBER`<br /><br /> `MDACTION_COORDINATE_SET`<br /><br /> `MDACTION_COORDINATE_CELL`|  
|`Hierarchy`|`MDACTION_COORDINATE_DIMENSION`|  
|`Level`|`MDACTION_COORDINATE_LEVEL`|  
|`Member`|`MDACTION_COORDINATE_MEMBER`|  
|`Set`|`MDACTION_COORDINATE_SET`|  
|`cell`|`MDACTION_COORDINATE_CELL`|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB for OLAP 架构行集](ole-db-for-olap-schema-rowsets.md)  
  
  
