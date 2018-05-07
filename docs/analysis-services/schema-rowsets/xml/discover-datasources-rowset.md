---
title: DISCOVER_DATASOURCES 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6ebbc52708591c54f9236aabcd2404c01a65e81f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="discoverdatasources-rowset"></a>DISCOVER_DATASOURCES 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  返回服务器或 Web 服务上可用的 XML for Analysis (XMLA) 访问接口数据源的列表。 发布的数据源从应用程序 Web 服务器的 URL 返回。 客户端可以连接到该列表中的一个数据源。  
  
 如果调用[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法替换**DISCOVER_DATASOURCES**中的枚举值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)元素，**发现**方法返回**DISCOVER_DATASOURCES**行集。  
  
 **适用于：**表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 客户端通过设置中选择数据源**DataSourceInfo**中的属性[属性](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)一起发送的元素[命令](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)元素[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。 客户端不应构造的内容**DataSourceInfo**属性发送到服务器。 相反，客户端应使用**发现**方法来查找该提供程序支持的数据源。 客户端然后发回相同的值**DataSourceInfo**属性，可从它获取**DISCOVER_DATASOURCES**行集。  
  
 **DISCOVER_DATASOURCES**行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DataSourceName**|**DBTYPE_WSTR**|是|数据源名称，如**Adventure Works**。|  
|**DataSourceDescription**|**DBTYPE_WSTR**||发布服务器输入的数据源的说明。<br /><br /> 可能会返回**NULL**。|  
|**URL**|**DBTYPE_WSTR**|是|显示为该数据源调用 XML for Analysis (XMLA) 方法的位置的唯一路径。<br /><br /> 可能会返回**NULL**。|  
|**DataSourceInfo**|**DBTYPE_WSTR**||包含连接到数据源所需的任何附加信息的字符串。<br /><br /> 可能会返回**NULL**。|  
|**ProviderName**|**DBTYPE_WSTR**|是|数据源的访问接口的名称。<br /><br /> 例如：`"MSOLAP"`<br /><br /> 可能会返回**NULL**。|  
|**提供程序类型**|**DBTYPE_WSTR**|是|访问接口支持的数据的类型。 此数组可包含一个或多个以下类型：<br /><br /> **MDP**： 多维数据提供程序。<br /><br /> **TDP**： 表格数据提供程序。<br /><br /> **DMP**： 数据挖掘提供程序 （实现 OLE DB for Data Mining 规范）。|  
|**AuthenticationMode**|**DBTYPE_WSTR**|是|数据源使用的安全模式类型的规范。 可以是下列值之一：<br /><br /> **未经身份验证**： 没有用户 ID 或密码已发送。<br /><br /> **身份验证**： 必须连接到数据源所需的信息中包含用户 ID 和密码。<br /><br /> **集成**： 数据源使用的基础安全来确定授权，例如所提供的集成安全性[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Internet 信息服务 (IIS)。|  
  
 未对此架构行集进行排序。  
  
> [!IMPORTANT]  
>  **DISCOVER_DATASOURCES**不能使用 DMV 查询和选择的命令语法查询行集。 但是， **DISCOVER_DATASOURCES**可以使用查询行集<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|值|  
|--------------|-----------|  
|GUID|06c03d41-f66d-49f3-b1b8-987f7af4cf18|  
|ADOMDNAME|DataSources|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
