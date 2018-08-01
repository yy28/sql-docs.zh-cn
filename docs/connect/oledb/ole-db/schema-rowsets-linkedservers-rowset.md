---
title: LINKEDSERVERS 行集 (OLE DB) |Microsoft Docs
description: LINKEDSERVERS 行集 (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- LINKEDSERVERS rowset
- enumerating data sources [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: c6b1299005c0307f04f0f245f6e0ec6ee57b5063
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2018
ms.locfileid: "39105763"
---
# <a name="schema-rowsets---linkedservers-rowset"></a>架构行集 - LINKEDSERVERS 行集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  LINKEDSERVERS 行集用于枚举可以参与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分布式查询的组织数据源。  
  
 LINKEDSERVERS 行集包含以下列。  
  
|列名|类型指示符|描述|  
|-----------------|--------------------|-----------------|  
|SVR_NAME|DBTYPE_WSTR|链接服务器的名称。|  
|SVR_PRODUCT|DBTYPE_WSTR|标识由链接服务器的名称所表示的数据存储的类型的制造商或其他名称。|  
|SVR_PROVIDERNAME|DBTYPE_WSTR|用于从服务器使用数据的 OLE DB 访问接口的友好名称。|  
|SVR_DATASOURCE|DBTYPE_WSTR|用于从提供程序获得数据源的 OLE DB DBPROP_INIT_DATASOURCE 字符串。|  
|SVR_PROVIDERSTRING|DBTYPE_WSTR|用于从提供程序获得数据源的 OLE DB DBPROP_INIT_PROVIDERSTRING 值。|  
|SVR_LOCATION|DBTYPE_WSTR|用于从提供程序获得数据源的 OLE DB DBPROP_INIT_LOCATION 字符串。|  
  
 行集按 SRV_NAME 排序，并支持对 SRV_NAME 的单个限制。  
  
## <a name="see-also"></a>另请参阅  
 [架构行集支持 (OLE DB)](../../oledb/ole-db/schema-rowset-support-ole-db.md)  
  
  
