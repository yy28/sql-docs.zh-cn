---
title: STSrid（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STSrid (geography Data Type)
- STSrid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSrid method
ms.assetid: 6b04f5a7-2e69-4d34-901e-b61ba6ca9c14
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 96a8577d621b9cc8b22e0f3b334b1d9831fdcad7
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2019
ms.locfileid: "65939162"
---
# <a name="stsrid-geography-data-type"></a>STSrid（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  STSrid 是一个表示该实例的空间引用标识符 (SRID) 的整数。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STSrid  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型：int  
  
 CLR 类型：**SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 此属性可以进行修改。  
  
## <a name="examples"></a>示例  
 第一个示例创建 SRID 值为 4326 (WGS84) 的 `geography` 实例并使用 `STSrid` 来确认该 SRID。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STSrid;  
```  
  
 第二个示例使用 `STSrid` 将实例的 SRID 值更改为 4267 (NAD27)，然后确认修改后的 SRID 值。  
  
```  
SET @g.STSrid = 4267;  
SELECT @g.STSrid;  
```  
  
## <a name="see-also"></a>另请参阅  
 [Geography 实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)   
 [空间引用标识符 (SRID)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
  
