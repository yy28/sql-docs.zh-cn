---
title: DISCOVER_INSTANCES 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0acc45eb2ea114a8d1c685aa6b3e867a4eaa967d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032898"
---
# <a name="discoverinstances-rowset"></a>DISCOVER_INSTANCES 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|**实例名称**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
