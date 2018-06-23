---
title: DISCOVER_DATASOURCES 行集 |Microsoft 文档
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
- DISCOVER_DATASOURCES
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_DATASOURCES rowset
ms.assetid: f3ff26ab-a447-416b-ba54-1716df2283de
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 32e7aa7327cce301cc8415f45635fda651d861f2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015793"
---
# <a name="discoverdatasources-rowset"></a>DISCOVER_DATASOURCES 行集
  返回服务器或 Web 服务上可用的 XML for Analysis (XMLA) 访问接口数据源的列表。 发布的数据源从应用程序 Web 服务器的 URL 返回。 客户端可以连接到该列表中的一个数据源。  
  
 如果调用[发现](../../xmla/xml-elements-methods-discover.md)方法替换`DISCOVER_DATASOURCES`中的枚举值[RequestType](../../xmla/xml-elements-properties/type-element-xmla.md)元素，`Discover`方法返回`DISCOVER_DATASOURCES`行集。  
  
 **适用于：** 表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 客户端通过设置中选择数据源`DataSourceInfo`中的属性[属性](../../xmla/xml-elements-properties/properties-element-xmla.md)一起发送的元素[命令](../../xmla/xml-elements-properties/command-element-xmla.md)元素[执行](../../xmla/xml-elements-methods-execute.md)方法。 客户端不应将构造的 `DataSourceInfo` 属性的内容发送到服务器， 而是应使用 `Discover` 方法查找访问接口支持的数据源， 然后，再将从 `DataSourceInfo` 行集获取的同一 `DISCOVER_DATASOURCES` 属性值发回。  
  
 `DISCOVER_DATASOURCES`行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`DataSourceName`|`DBTYPE_WSTR`|是|数据源的名称，如 `Adventure Works`。|  
|`DataSourceDescription`|`DBTYPE_WSTR`||发布服务器输入的数据源的说明。<br /><br /> 可能会返回 `NULL`。|  
|`URL`|`DBTYPE_WSTR`|是|显示为该数据源调用 XML for Analysis (XMLA) 方法的位置的唯一路径。<br /><br /> 可能会返回 `NULL`。|  
|`DataSourceInfo`|`DBTYPE_WSTR`||包含连接到数据源所需的任何附加信息的字符串。<br /><br /> 可能会返回 `NULL`。|  
|`ProviderName`|`DBTYPE_WSTR`|是|数据源的访问接口的名称。<br /><br /> 例如：`"MSOLAP"`<br /><br /> 可能会返回 `NULL`。|  
|`ProviderType`|`DBTYPE_WSTR`|是|访问接口支持的数据的类型。 此数组可包含一个或多个以下类型：<br /><br /> `MDP`：多维数据访问接口。<br /><br /> `TDP`：表格数据访问接口。<br /><br /> `DMP`：数据挖掘访问接口（实现 OLE DB for Data Mining 规范）。|  
|`AuthenticationMode`|`DBTYPE_WSTR`|是|数据源使用的安全模式类型的规范。 可以是下列值之一：<br /><br /> `Unauthenticated`：不必发送用户 ID 或密码。<br /><br /> `Authenticated`：连接数据源所需的信息中必须包括用户 ID 和密码。<br /><br /> `Integrated`：数据源使用基础安全性确定授权，如 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS) 提供的集成安全性。|  
  
 未对此架构行集进行排序。  
  
> [!IMPORTANT]  
>  不能使用 DMV 查询和 SELECT 命令语法查询 `DISCOVER_DATASOURCES` 行集。 但是，可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A> 查询 `DISCOVER_DATASOURCES` 行集。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|06c03d41-f66d-49f3-b1b8-987f7af4cf18|  
|ADOMDNAME|DataSources|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)  
  
  