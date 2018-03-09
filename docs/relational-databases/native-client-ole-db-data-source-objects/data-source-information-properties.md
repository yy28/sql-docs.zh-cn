---
title: "数据源信息属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-data-source-objects
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 7fd80e47-5bd9-41e2-a3d3-091a7c8c5f2b
caps.latest.revision: "37"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9db499b31ef91d05d6f37d110376075efbb96b52
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="data-source-information-properties"></a>数据源信息属性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在特定于访问接口的属性集 DBPROPSET_SQLSERVERDATASOURCEINFO 中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口定义了以下数据源信息属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|类型：VT_BOOL<br /><br /> 读取/写入：读取<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明：用于确定是否支持列排序规则。<br /><br /> VARIANT_TRUE：支持列级别排序规则。<br /><br /> VARIANT_FALSE：不支持列级别排序规则。|  
|SSPROP_UNICODELCID|类型：VT_I4 读取/写入：读取<br /><br /> 说明：Unicode 区域设置 ID。<br /><br /> 这是用于 Unicode 数据排序的区域设置。|  
|SSPROP_UNICODECOMPARISONSTYLE|类型：VT_I4 读取/写入：读取<br /><br /> 说明：Unicode 比较样式。<br /><br /> 用于 Unicode 数据排序的排序选项。|  
  
 在特定于访问接口的属性集 DBPROPSET_SQLSERVERSTREAM 中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口定义了以下附加属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|类型：VT_BSTR 读取/写入：读取/写入<br /><br /> 说明：FOR XML 查询的结果可能不是格式正确的文档。 指定此属性是、 的结果选择... 对于 XML 查询包装在提供此属性以返回格式正确的 XML 文档的根标记中。 如果查询是在浏览器中执行的，在加载结果时它可能导致浏览器显示分析器错误。 为了避免错误，SQL ISAPI 支持 ROOT 关键字。 此关键字映射到 SSPROP_STREAM_XMLROOT 属性。|  
  
## <a name="see-also"></a>另请参阅  
 [数据源对象 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
