---
title: 会话属性-SQL Server Native Client OLE DB 提供程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d17b673a12a915318e523000081fcd6114e8185c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128552"
---
# <a name="session-properties---sql-server-native-client-ole-db-provider"></a>会话属性 - SQL Server Native Client OLE DB 提供程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将按如下所示解释 OLE DB 会话属性。  
  
|属性 ID|描述|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持所有自动提交事务隔离级别，混沌级别 DBPROPVAL_TI_CHAOS 除外。|  
  
 在特定于提供程序的属性集 DBPROPSET_SQLSERVERSESSION 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口定义以下附加的会话属性。  
  
|属性 ID|描述|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|键入：VT_BOOL<br /><br /> R/W:读/写<br /><br /> 默认：VARIANT_FALSE<br /><br /> 说明:带引号的标识符允许在 CATALOG 限制中。<br /><br /> VARIANT_TRUE:提供分布式的查询支持的架构行集的目录限制识别带引号的标识符。<br /><br /> VARIANT_FALSE:无法提供分布式的查询支持的架构行集的目录限制识别带引号的标识符。<br /><br /> 有关提供分布式查询支持的架构行集的详细信息，请参阅[架构行集中的分布式查询支持](../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md)。|  
|SSPROP_ALLOWNATIVEVARIANT|键入：VT_BOOL<br /><br /> R/W:读/写<br /><br /> 默认：VARIANT_FALSE<br /><br /> 说明:确定在提取的数据是作为 DBTYPE_VARIANT 还是作为 DBTYPE_SQLVARIANT。<br /><br /> VARIANT_TRUE:作为 dbtype_sqlvariant 时，在这种情况下缓冲区将保留 SSVARIANT 结构返回列类型。<br /><br /> VARIANT_FALSE:列类型作为 DBTYPE_VARIANT 返回，并将缓冲区将具有 VARIANT 结构。|  
|SSPROP_ASYNCH_BULKCOPY|若要使用异步模式，请在调用 BCPExec 方法之前，将特定于提供程序的会话属性 SSPROP_ASYNCH_BULKCOPY 设置为 VARIANT_TRUE。 此属性位于 DBPROPSET_SQLSERVERSESSION 属性集中。|  
  
## <a name="see-also"></a>请参阅  
 [数据源对象&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
