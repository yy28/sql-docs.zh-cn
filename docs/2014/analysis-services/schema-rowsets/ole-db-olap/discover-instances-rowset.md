---
title: DISCOVER_INSTANCES 行集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DISCOVER_INSTANCES
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_INSTANCES rowset
ms.assetid: e0842e63-089d-468d-869f-634da343d9fb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a0f716f32898668e019db15aef62e140e9c0d09
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198578"
---
# <a name="discoverinstances-rowset"></a>DISCOVER_INSTANCES 行集
  介绍服务器上的实例。  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_INSTANCES`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`INSTANCE_NAME`|`DBTYPE_WSTR`||实例的名称。|  
|`INSTANCE_PORT_NUMBER`|`DBTYPE_I4`||实例侦听的端口号。|  
|`INSTANCE_STATE`|`DBTYPE_I4`||服务器实例的状态：<br /><br /> -   `Started`<br />-   `Stopped`<br />-   `Starting`<br />-   `Stopping`<br />-   `Paused`|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 `DISCOVER_INSTANCES`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`INSTANCE_NAME`|`DBTYPE_WSTR`|可选。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB for OLAP 架构行集](ole-db-for-olap-schema-rowsets.md)  
  
  
