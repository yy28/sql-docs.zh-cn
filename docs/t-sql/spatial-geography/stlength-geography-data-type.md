---
title: STLength（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLength (geography Data Type)
- STLength_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLength method
ms.assetid: 774560ab-4a4a-4058-b043-1e67cf6fb9eb
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 61487b976322f8725f9398e54f8292919ff0ca58
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139112"
---
# <a name="stlength-geography-data-type"></a>STLength（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回 geography 实例中元素的总长度或 GeometryCollection 内的 geography 实例的总长度    。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：float   
  
 CLR 返回类型：**SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 如果 geography 实例是闭合的，则其长度按围绕该实例的总长度进行计算；任何多边形的长度为其周长，点的长度为 0  。 GeometryCollection 的长度通过计算该集合内包含的所有 geography 实例的长度和得到   。  
  
 STLength() 对有效和无效的 LineString 均适用。 通常，LineString 会因可能由 GPS 跟踪不准确之类的异常引起的段重叠而无效。 STLength() 不会删除重叠或无效的段。 它将重叠和无效的段包括在其返回的长度值中。 MakeValid() 方法可以从 LineString 中删除重叠段。  
  
## <a name="examples"></a>示例  
 下面的示例创建 `LineString` 实例并使用 `STLength()` 确定该实例的长度。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
