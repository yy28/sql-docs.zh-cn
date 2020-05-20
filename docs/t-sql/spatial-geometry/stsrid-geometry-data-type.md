---
title: STSrid（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STSrid (geometry Data Type)
- STSrid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSrid (geometry Data Type)
ms.assetid: 5e0de983-a0fe-48b7-9e08-30588d7271e2
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f1119c0c906e3a3825882e3fe1043e9bdaceb0f9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68066301"
---
# <a name="stsrid-geometry-data-type"></a>STSrid（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **STSrid** 是一个整数，表示实例的空间引用标识符。  
  
此属性可以进行修改。
  
## <a name="syntax"></a>语法  
  
```  
  
STSrid  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型：int   
  
 CLR 类型：SqlInt32   
  
## <a name="examples"></a>示例  
 第一个示例创建 SRID 值为 13 的 geometry 实例并使用 `STSrid` 确认该 SRID。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0))', 13);  
SELECT @g.STSrid;  
```  
  
 第二个示例使用 `STSrid` 将该实例的 SRID 值更改为 23，然后确认修改后的 SRID 值。  
  
```  
SET @g.STSrid = 23;  
SELECT @g.STSrid;  
```  
  
## <a name="see-also"></a>另请参阅  
 [STX（geometry 数据类型）](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STY（geometry 数据类型）](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

