---
title: MDSCHEMA_INPUT_DATASOURCES 行集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_INPUT_DATASOURCES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_INPUT_DATASOURCES rowset
ms.assetid: 12482fd5-16e3-4171-9cb0-76d0d4f5308e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa2f372c4facb1b2e51561bbd82a8e35fe8ed134
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210027"
---
# <a name="mdschemainputdatasources-rowset"></a>MDSCHEMA_INPUT_DATASOURCES 行集
  介绍数据库中定义的数据源。  
  
## <a name="rowset-columns"></a>行集列  
 `MDSCHEMA_INPUT_DATASOURCES`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||此数据源所属目录的名称。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不提供支持。|  
|`DATASOURCE_NAME`|`DBTYPE_WSTR`||数据源对象的名称。|  
|`DATASOURCE_TYPE`|`DBTYPE_WSTR`||数据源的类型。 有效值包括：<br /><br /> -   `Relational`<br />-   `Olap`|  
|`CREATED_ON`|`DBTYPE_DBTIMESTAMP`||创建数据源的日期。|  
|`LAST_SCHEMA_UPDATE`|`DBTYPE_DBTIMESTAMP`||上次修改数据源的日期和时间。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||操作的用户友好说明。|  
|`TIMEOUT`|`DBTYPE_UI4`||数据源的超时值。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 `MDSCHEMA_INPUT_DATASOURCES`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|可选。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|可选。|  
|`DATASOURCE_NAME`|`DBTYPE_WSTR`|可选。|  
|`DATASOURCE_TYPE`|`DBTYPE_WSTR`|可选。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB for OLAP 架构行集](ole-db-for-olap-schema-rowsets.md)  
  
  
