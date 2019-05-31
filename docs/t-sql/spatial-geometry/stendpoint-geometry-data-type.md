---
title: STEndpoint（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STEndpoint (geometry Data Type)
- STEndpoint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STEndpoint (geometry Data Type)
ms.assetid: 61773c45-b568-4e0c-94da-1310c42de7f5
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: a51bb784c2cb4a9ef4ab54d46379d0dcc60d18b4
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2019
ms.locfileid: "65938964"
---
# <a name="stendpoint-geometry-data-type"></a>STEndpoint（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回 geometry 实例的终点  。
  
## <a name="syntax"></a>语法  
  
```  
  
.STEndPoint ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry   
  
 CLR 返回类型：**SqlGeometry**  
  
 开放地理空间联盟 (OGC) 类型：**Point**  
  
## <a name="remarks"></a>Remarks  
 `STEndPoint()` 等效于 [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md) (x.NumPoints())。  
  
 如果针对空 geometry 实例调用此方法，则此方法返回 Null  。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `LineString` 创建 `STGeomFromText()` 实例，并使用 `STEndpoint()` 检索 `LineString` 的终点。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STEndPoint().ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

