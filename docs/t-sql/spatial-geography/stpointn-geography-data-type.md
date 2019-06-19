---
title: STPointN（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN method
ms.assetid: 47670feb-b9e0-4b4b-af83-b9bba7da66ac
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 983442f724d4c2090bbface71a793bac71eb9ac7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65936088"
---
# <a name="stpointn-geography-data-type"></a>STPointN（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回 geography 实例中的指定点  。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 一个 int 表达式，其值介于 1 与 geography 实例中的点数之间   。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography   
  
 CLR 返回类型：**SqlGeography**  
  
 开放地理空间联盟 (OGC) 类型：**Point**  
  
## <a name="remarks"></a>Remarks  
 如果 geography 实例是用户创建的，则 STPointN() 返回由 expression 通过按照点的原始输入顺序对点进行排序而指定的点   。  
  
 如果 geography 实例是系统构建的，则 STPointN() 返回由 expression 通过按照点的输出顺序对所有点进行排序而指定的点，点的输出顺序为：首先按 geography 实例、然后按实例中的环（如果适用），最后按环中的点    。 此顺序是确定的。  
  
 如果使用小于 1 的值来调用此方法，则会引发 ArgumentOutOfRangeException  。  
  
 如果使用大于实例中点数的值来调用此方法，则返回 Null。  
  
## <a name="examples"></a>示例  
 下面的示例创建 `LineString` 实例，并使用 `STPointN()` 检索实例说明中的第二个点。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
