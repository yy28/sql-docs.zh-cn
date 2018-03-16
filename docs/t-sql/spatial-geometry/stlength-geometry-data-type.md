---
title: "STLength（geometry 数据类型）| Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
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
- STLength_TSQL
- STLength (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STLength (geometry Data Type)
ms.assetid: e34dc620-2a65-4248-b099-fff91830ab98
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4611b911e765135235f06fa656751e6cebd9ea18
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stlength-geometry-data-type"></a>STLength（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回 **geometry** 实例中的元素的总长度。
  
## <a name="syntax"></a>语法  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：float  
  
 CLR 返回类型：SqlDouble  
  
## <a name="remarks"></a>Remarks  
 如果 **geometry** 实例是闭合的，则其长度按围绕该实例的总长度进行计算；任何多边形的长度均为其周长，点的长度为 0。 任何 **geometrycollection** 类型的长度均为它所包含的 **geometry** 实例的长度之和。  
  
 STLength() 对有效和无效的 LineString 均适用。 通常，LineString 会因可能由 GPS 跟踪不准确之类的异常引起的段重叠而无效。 STLength() 不会删除重叠或无效的段。 它将重叠和无效的段包括在其返回的长度值中。 MakeValid() 方法可以从 LineString 中删除重叠段。  
  
## <a name="examples"></a>示例  
 下面的示例创建 `LineString` 实例并使用 `STLength()` 确定该实例的长度。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>另请参阅  
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

