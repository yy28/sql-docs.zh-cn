---
title: "STEndpoint（geography 数据类型）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STEndpoint (geography Data Type)
- STEndpoint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STEndpoint method
ms.assetid: 8974cd07-8ec4-4126-8fc2-fdcf322ccedd
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 910e11dc72d4bb0ec7a2d09a0217c4b9d7c12431
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stendpoint-geography-data-type"></a>STEndpoint（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回 geography 实例的终点。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STEndPoint ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography  
  
 CLR 返回类型：SqlGeography  
  
 开放地理空间信息联盟 (OGC) 类型：Point  
  
## <a name="remarks"></a>Remarks  
 STEndPoint() 等效于 [STPointN](../../t-sql/spatial-geography/stpointn-geography-data-type.md)`(x.STNumPoints``())`。  
  
 如果针对空 geography 实例调用此方法，则此方法返回 Null。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `LineString` 创建 `STGeomFromText()` 实例，并使用 `STEndpoint()` 检索 `LineString` 的终点。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STEndPoint().ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
