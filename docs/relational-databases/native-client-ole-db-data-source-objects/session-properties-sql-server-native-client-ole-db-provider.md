---
title: "会话属性-SQL Server Native Client OLE DB 提供程序 |Microsoft 文档"
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
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 78d46120895fc65bf9e0be8f419854731ecf3198
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="session-properties---sql-server-native-client-ole-db-provider"></a>会话属性-SQL Server Native Client OLE DB 提供程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将按以下方式解释 OLE DB 会话属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持混沌级别 DBPROPVAL_TI_CHAOS 除外的所有自动提交事务隔离级别。|  
  
 在提供程序特定属性将设置 DBPROPSET_SQLSERVERSESSION， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序定义以下其他会话属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|类型：VT_BOOL<br /><br /> 读/写︰ 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：在 CATALOG 限制中允许带引号的标识符。<br /><br /> VARIANT_TRUE：对提供分布式查询支持的架构行集的目录限制识别带引号的标识符。<br /><br /> VARIANT_FALSE：对提供分布式查询支持的架构行集的目录限制不识别带引号的标识符。<br /><br /> 有关提供分布式的查询支持的架构行集的详细信息，请参阅[分布式查询支持架构行集中](../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md)。|  
|SSPROP_ALLOWNATIVEVARIANT|类型：VT_BOOL<br /><br /> R/W：读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：确定提取的数据是作为 DBTYPE_VARIANT 还是作为 DBTYPE_SQLVARIANT。<br /><br /> VARIANT_TRUE：列类型作为 DBTYPE_SQLVARIANT 返回，这种情况下缓冲区将保留 SSVARIANT 结构。<br /><br /> VARIANT_FALSE：列类型作为 DBTYPE_VARIANT 返回，且缓冲区将具有 VARIANT 结构。|  
|SSPROP_ASYNCH_BULKCOPY|若要使用异步模式，请在调用 BCPExec 方法之前，将特定于提供程序的会话属性 SSPROP_ASYNCH_BULKCOPY 设置为 VARIANT_TRUE。 此属性位于 DBPROPSET_SQLSERVERSESSION 属性集中。|  
  
## <a name="see-also"></a>另请参阅  
 [数据源对象 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
