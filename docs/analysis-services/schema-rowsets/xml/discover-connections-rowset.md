---
title: DISCOVER_CONNECTIONS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4bb236b6d69199bd4c488c365ba108fc3913f02c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34028007"
---
# <a name="discoverconnections-rowset"></a>DISCOVER_CONNECTIONS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  提供服务器上当前打开的连接的资源使用情况和活动信息。  
  
 **适用于：** 表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_CONNECTIONS**行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|------------------|-----------------|  
|**CONNECTION_ID**|**DBTYPE_I4**|是|标识连接的唯一编号。|  
|**CONNECTION_USER_NAME**|**DBTYPE_WSTR**|是|连接的用户名。|  
|**CONNECTION_IMPERSONATED_USER_NAME**|**DBTYPE_WSTR**|是|保留供将来使用。 Analysis Services 始终为 CONNECTION_IMPERSONATED_USER_NAME 的值返回 NULL。|  
|**CONNECTION_HOST_NAME**|**DBTYPE_WSTR**|是|启动连接的计算机名称。|  
|**CONNECTION_HOST_APPLICATION**|**DBTYPE_WSTR**||启动连接的应用程序名称。|  
|**CONNECTION_START_TIME**|**DBTYPE_DBTIMESTAMP**||启动连接时的服务器 UTC 日期和时间。|  
|**CONNECTION_ELAPSED_TIME_MS**|**DBTYPE_I8**|是|自连接开始起经过的时间（毫秒）。|  
|**CONNECTION_LAST_COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||服务器 UTC 日期和最后一个命令开始其执行时间。|  
|**CONNECTION_LAST_COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||上次命令执行结束时的服务器 UTC 日期和时间。|  
|**CONNECTION_LAST_COMMAND_ELAPSED_TIME_MS**|**DBTYPE_I8**|是|自上次命令执行结束后经过的时间（毫秒）。|  
|**CONNECTION_IDLE_TIME_MS**|**DBTYPE_I8**|是|自连接开始后的空闲时间（毫秒）。|  
|**CONNECTION_BYTES_SENT**|**DBTYPE_I8**||自连接开始后该连接发送的累计字节数。|  
|**CONNECTION_DATA_BYTES_SENT**|**DBTYPE_I8**||自连接开始后该连接发送的累计数据字节数。<br /><br /> 数据在连接中以压缩方式传送；此值表示解压缩后的发送数据。|  
|**CONNECTION_BYTES_RECEIVED**|**DBTYPE_I8**||自连接开始后该连接收到的累计字节数。|  
|**CONNECTION_DATA_BYTES_RECEIVED**|**DBTYPE_I8**||自连接开始后该连接收到的累计数据字节数。<br /><br /> 数据在连接中以压缩方式传送；此值表示解压缩后的接收数据。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|值|  
|--------------|-----------|  
|GUID|a07ccd25-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|连接|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
