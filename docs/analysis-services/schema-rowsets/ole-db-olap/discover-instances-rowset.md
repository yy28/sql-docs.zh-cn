---
title: "DISCOVER_INSTANCES 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DISCOVER_INSTANCES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_INSTANCES rowset
ms.assetid: e0842e63-089d-468d-869f-634da343d9fb
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fbed6de71f83da959591003039fe5910a1a4c53d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="discoverinstances-rowset"></a>DISCOVER_INSTANCES 行集
  介绍服务器上的实例。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_INSTANCES**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**实例名称**|**DBTYPE_WSTR**||实例的名称。|  
|**INSTANCE_PORT_NUMBER**|**DBTYPE_I4**||实例侦听的端口号。|  
|**INSTANCE_STATE**|**DBTYPE_I4**||服务器实例的状态：<br /><br /> **启动**<br /><br /> **已停止**<br /><br /> **启动**<br /><br /> **停止**<br /><br /> **已暂停**|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_INSTANCES**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**实例名称**|**DBTYPE_WSTR**|可选。|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

