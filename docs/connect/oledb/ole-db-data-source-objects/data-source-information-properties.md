---
title: 数据源信息属性 |Microsoft Docs
description: 数据源信息属性
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 18518e92896223201c24982c6b6f0955ea81aa6f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66768619"
---
# <a name="data-source-information-properties"></a>数据源信息属性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  在提供程序特定的属性集 DBPROPSET_SQLSERVERDATASOURCEINFO 中，适用于 SQL Server 的 OLE DB 驱动程序定义了下列数据源信息属性。  
  
|属性 ID|描述|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|类型：VT_BOOL<br /><br /> 读取/写入：读取<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明：用于确定是否支持列排序规则。<br /><br /> VARIANT_TRUE：支持列级别排序规则。<br /><br /> VARIANT_FALSE：不支持列级别排序规则。|  
|SSPROP_UNICODELCID|类型：VT_I4 读取/写入：读取<br /><br /> 说明：Unicode 区域设置 ID。<br /><br /> 这是用于 Unicode 数据排序的区域设置。|  
|SSPROP_UNICODECOMPARISONSTYLE|类型：VT_I4 读取/写入：读取<br /><br /> 说明：Unicode 比较样式。<br /><br /> 用于 Unicode 数据排序的排序选项。|  
  
 在提供程序特定的属性集 DBPROPSET_SQLSERVERSTREAM 中，适用于 SQL Server 的 OLE DB 驱动程序定义了下列附加属性。  
  
|属性 ID|描述|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|类型：VT_BSTR 读取/写入：读取/写入<br /><br /> 说明：FOR XML 查询的结果可能不是格式正确的文档。 如果此属性已指定，“select ... for XML”查询结果会被包装在此属性提供的根标记中，以返回格式正确的 XML 文档。 如果查询是在浏览器中执行的，在加载结果时它可能导致浏览器显示分析器错误。 为了避免错误，SQL ISAPI 支持 ROOT 关键字。 此关键字映射到 SSPROP_STREAM_XMLROOT 属性。|  
  
## <a name="see-also"></a>另请参阅  
 [数据源对象&#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
