---
title: 数据源信息属性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 7fd80e47-5bd9-41e2-a3d3-091a7c8c5f2b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 946c6d39bd02bbccd898262da6642813fbb3c94f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52543995"
---
# <a name="data-source-information-properties"></a>数据源信息属性
  在特定于访问接口的属性集 DBPROPSET_SQLSERVERDATASOURCEINFO 中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口定义了以下数据源信息属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|键入：VT_BOOL<br /><br /> R/W：读取<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明:用于确定是否支持列排序规则。<br /><br /> VARIANT_TRUE：支持列级排序规则。<br /><br /> VARIANT_FALSE：不支持列级排序规则。|  
|SSPROP_UNICODELCID|键入：VT_I4 R/W:读取<br /><br /> 说明:Unicode 区域设置 id。<br /><br /> 这是用于 Unicode 数据排序的区域设置。|  
|SSPROP_UNICODECOMPARISONSTYLE|键入：VT_I4 R/W:读取<br /><br /> 说明:Unicode 比较样式。<br /><br /> 用于 Unicode 数据排序的排序选项。|  
  
 在特定于访问接口的属性集 DBPROPSET_SQLSERVERSTREAM 中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口定义了以下附加属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|键入：VT_BSTR R/W:读/写<br /><br /> 说明:FOR XML 查询的结果可能不是格式正确的文档。 如果此属性已指定，“select ... for XML”查询结果会被包装在此属性提供的根标记中，以返回格式正确的 XML 文档。 如果查询是在浏览器中执行的，在加载结果时它可能导致浏览器显示分析器错误。 为了避免错误，SQL ISAPI 支持 ROOT 关键字。 此关键字映射到 SSPROP_STREAM_XMLROOT 属性。|  
  
## <a name="see-also"></a>请参阅  
 [数据源对象&#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
