---
title: LINKEDSERVERS 行集 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- LINKEDSERVERS rowset
- enumerating data sources [OLE DB]
ms.assetid: 2633fd8a-65e7-498d-9aed-8e4b1cca2381
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a136e3b2064e42e6bae7cfb39f059dbaa41a8410
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62667332"
---
# <a name="linkedservers-rowset-ole-db"></a>LINKEDSERVERS 行集 (OLE DB)
  LINKEDSERVERS 行集用于枚举可以参与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分布式查询的组织数据源****。  
  
 LINKEDSERVERS 行集包含以下列****。  
  
|列名称|类型指示符|说明|  
|-----------------|--------------------|-----------------|  
|SVR_NAME|DBTYPE_WSTR|链接服务器的名称。|  
|SVR_PRODUCT|DBTYPE_WSTR|标识由链接服务器的名称所表示的数据存储的类型的制造商或其他名称。|  
|SVR_PROVIDERNAME|DBTYPE_WSTR|用于从服务器使用数据的 OLE DB 访问接口的友好名称。|  
|SVR_DATASOURCE|DBTYPE_WSTR|用于从提供程序获得数据源的 OLE DB DBPROP_INIT_DATASOURCE 字符串。|  
|SVR_PROVIDERSTRING|DBTYPE_WSTR|用于从提供程序获得数据源的 OLE DB DBPROP_INIT_PROVIDERSTRING 值。|  
|SVR_LOCATION|DBTYPE_WSTR|用于从提供程序获得数据源的 OLE DB DBPROP_INIT_LOCATION 字符串。|  
  
 行集按 SRV_NAME 排序，并支持对 SRV_NAME 的单个限制。  
  
## <a name="see-also"></a>另请参阅  
 [架构行集支持 (OLE DB)](schema-rowset-support-ole-db.md)  
  
  
