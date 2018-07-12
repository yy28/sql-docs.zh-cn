---
title: 会话属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6a26faf8673ff110e079d4606e587e079f33025
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413356"
---
# <a name="session-properties"></a>会话属性
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将按如下所示解释 OLE DB 会话属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持所有自动提交事务隔离级别，混沌级别 DBPROPVAL_TI_CHAOS 除外。|  
  
 在特定于提供程序的属性集 DBPROPSET_SQLSERVERSESSION 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口定义以下附加的会话属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|类型：VT_BOOL<br /><br /> R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：在 CATALOG 限制中允许带引号的标识符。<br /><br /> VARIANT_TRUE：对提供分布式查询支持的架构行集的目录限制识别带引号的标识符。<br /><br /> VARIANT_FALSE：对提供分布式查询支持的架构行集的目录限制不识别带引号的标识符。<br /><br /> 有关提供分布式的查询支持的架构行集的详细信息，请参阅[分布式查询支持架构行集中](../native-client/ole-db/schema-rowsets-distributed-query-support.md)。|  
|SSPROP_ALLOWNATIVEVARIANT|类型：VT_BOOL<br /><br /> R/W：读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：确定提取的数据是作为 DBTYPE_VARIANT 还是作为 DBTYPE_SQLVARIANT。<br /><br /> VARIANT_TRUE：列类型作为 DBTYPE_SQLVARIANT 返回，这种情况下缓冲区将保留 SSVARIANT 结构。<br /><br /> VARIANT_FALSE：列类型作为 DBTYPE_VARIANT 返回，且缓冲区将具有 VARIANT 结构。|  
|SSPROP_ASYNCH_BULKCOPY|若要使用异步模式，请在调用 BCPExec 方法之前，将特定于提供程序的会话属性 SSPROP_ASYNCH_BULKCOPY 设置为 VARIANT_TRUE。 此属性位于 DBPROPSET_SQLSERVERSESSION 属性集中。|  
  
## <a name="see-also"></a>请参阅  
 [数据源对象&#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
