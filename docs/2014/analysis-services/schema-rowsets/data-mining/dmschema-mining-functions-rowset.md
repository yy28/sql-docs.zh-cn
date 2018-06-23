---
title: DMSCHEMA_MINING_FUNCTIONS 行集 |Microsoft 文档
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
api_name:
- DMSCHEMA_MINING_FUNCTIONS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_FUNCTIONS rowset
ms.assetid: 9ace7493-a7b1-45ca-93de-3cb2f3597017
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b5a60e18a57c15976e7a7bd5d5e31729e255869a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128417"
---
# <a name="dmschemaminingfunctions-rowset"></a>DMSCHEMA_MINING_FUNCTIONS 行集
  介绍可在正在运行的服务器上的数据挖掘算法支持的数据挖掘函数[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="rowset-columns"></a>行集列  
 `DMSCHEMA_MINING_FUNCTIONS`行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||算法的名称。|  
|`FUNCTION_NAME`|`DBTYPE_WSTR`||函数的名称。|  
|`FUNCTION_SIGNATURE`|`DBTYPE_WSTR`||函数的签名。|  
|`RETURNS_TABLE`|`DBTYPE_BOOL`||如果函数返回标量内容（如字符参数的长度），则为 `FALSE`；如果函数返回表（如直方图表），则为 `TRUE`。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||函数的用户友好说明。|  
|`HELP_FILE`|`DBTYPE_WSTR`||包含此函数文档的文件的名称。|  
|`HELP_CONTEXT`|`DBTYPE_I4`||此函数的帮助上下文 ID。|  
  
## <a name="restriction-columns"></a>限制列  
 `DMSCHEMA_MINING_FUNCTIONS`行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|可选。|  
|`FUNCTION_NAME`|`DBTYPE_WSTR`|可选。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘架构行集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  