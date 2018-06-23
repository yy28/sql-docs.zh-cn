---
title: DBSCHEMA_TABLES 行集 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DBSCHEMA_TABLES
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_TABLES rowset
ms.assetid: 14c16e6b-0aff-4ad1-b98f-cdb7df0f8d73
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9033dc2f48b74bc13268d06f66a084f4ada22cfc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029323"
---
# <a name="dbschematables-rowset"></a>DBSCHEMA_TABLES 行集
  标识的度量值组和维度中的表作为公开[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="rowset-columns"></a>行集列  
 `DBSCHEMA_TABLES`行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|255|此对象所属目录的名称。|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|255|此对象所属多维数据集的名称。|  
|`TABLE_NAME`|`DBTYPE_WSTR`|255|对象的名称，条件是 `TABLE_TYPE` 为 `TABLE`。|  
|`TABLE_TYPE`|`DBTYPE_WSTR`||表的类型。<br /><br /> `TABLE` 指示对象是度量值组。<br /><br /> `SYSTEM TABLE` 指示对象是一个维度。|  
|`TABLE_GUID`|`DBTYPE_GUID`||不提供支持。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||用户可以阅读的对象说明。|  
|`TABLE_PROPID`|`DBTYPE_UI4`||不提供支持。|  
|`DATE_CREATED`|`DBTYPE_DBTIMESTAMP`||不提供支持。|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||上次修改对象的日期。|  
|`TABLE_OLAP_TYPE`|`DBTYPE_WSTR`||对象的 OLAP 类型。<br /><br /> **MEASURE_GROUP**指示对象是度量值组。<br /><br /> `CUBE_DIMENSION` 指示对象为维度。|  
  
 行集按 `TABLE_TYPE`、`TABLE_CATALOG`、`TABLE_SCHEMA` 和 `TABLE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制列  
 `DBSCHEMA_TABLES`行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|可选|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|可选|  
|`TABLE_NAME`|`DBTYPE_WSTR`|可选|  
|`TABLE_TYPE`|`DBTYPE_WSTR`|可选|  
|`TABLE_OLAP_TYPE`|`DBTYPE_WSTR`|可选|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB 架构行集](ole-db-schema-rowsets.md)  
  
  