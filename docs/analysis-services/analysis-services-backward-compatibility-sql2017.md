---
title: SQL Server 2017 Analysis Services 向后兼容性 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: e7903de787a1b63627bca8da23369fbee9014c6e
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685734"
---
# <a name="analysis-services-backward-compatibility-sql-2017"></a>Analysis Services 向后兼容性 (SQL 2017)
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

本文描述了中功能可用性和当前版本和以前的版本之间行为的更改。

## <a name="deprecated-features"></a>已弃用的功能
一个*弃用的功能*将停用从产品中未来版本中，但仍支持并包含在当前版本，以保持向后兼容性。 建议您停止使用新的和现有项目中已弃用的功能以保持与将来的版本兼容。 文档不会更新为已弃用的功能。

在此版本中已弃用以下功能：
  
|||  
|-|-|  
|**模式/类别**|**功能**|
|多维|数据挖掘|
|多维|远程链接的度量值组|
|表格|1100年和 1103年兼容级别模型|
|表格|表格对象模型属性：Column.TableDetailPosition, Column.IsDefaultLabel, Column.IsDefaultImage|
|工具|SQL Server Profiler for Trace Capture<br /><br /> 替代功能使用 SQL Server Management Studio 中嵌入的扩展事件探查器。  <br /> 请参阅 [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)。|  
|工具|跟踪重播 <br />替代功能的 Server Profiler。 没有替代功能。|  
|跟踪管理对象和跟踪 API|Microsoft.AnalysisServices.Trace 对象（包含 Analysis Services 跟踪和重播对象的 API）。 替代功能由多个部分组成：<br /><br /> -跟踪配置：Microsoft.SqlServer.Management.XEvent<br />-跟踪读取：Microsoft.SqlServer.XEvent.Linq<br />-跟踪重播：None|  


## <a name="discontinued-features"></a>废弃的功能
一个*停用功能*在早期版本中已弃用。 它包含在当前版本中，可以继续但不再受支持。 废弃的功能可能会删除完全在以后发布或更新。

以下功能在早期版本中已弃用，不再支持此版本中。
  
|||  
|-|-|  
|**模式/类别**|**功能**|  
|表格|VertipaqPagingPolicy 内存属性值 (2)，启用分页到磁盘使用的内存映射文件。|
|多维|远程分区|  
|多维|远程链接的度量值组|  
|多维|维度写回|  
|多维|链接的维度|


## <a name="breaking-changes"></a>重大更改
一个*重大更改*导致的当前版本升级后的功能、 数据模型、 应用程序代码或将脚本保存到不再工作。

在此版本中没有重大更改。

## <a name="behavior-changes"></a>行为更改
一个*行为更改*影响相同的功能与以前的版本相比的当前版本中的工作方式。 描述了仅重要行为更改。 不包括用户界面中的更改。

更改 MDSCHEMA_MEASUREGROUP_DIMENSIONS 和 DISCOVER_CALC_DEPENDENCY，详述[什么是 Analysis Services 的 SQL Server 2017 CTP 2.1 中的新增功能](https://blogs.msdn.microsoft.com/analysisservices/2017/05/18/whats-new-in-sql-server-2017-ctp-2-1-for-analysis-services/)公告。


## <a name="see-also"></a>另请参阅
[Analysis Services 向后兼容性 (SQL Server 2016)](analysis-services-backward-compatibility.md)
