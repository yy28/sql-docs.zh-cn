---
title: AsBinaryZM（geometry 数据类型）| Microsoft 文档
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- AsBinaryZM geometry
ms.assetid: 5eae2872-adca-4b8f-8b04-4ee91ced98f1
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: feafda7b9ed7fd7ca61310df5d29b0330a521d3b
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2019
ms.locfileid: "65935957"
---
# <a name="asbinaryzm-geometry-datatype"></a>AsBinaryZM（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回 geometry 实例的开放地理空间信息联盟 (OGC) 已知二进制 (WKB) 表示形式，增加了该实例传递的任何 Z（标高）和 M（度量）值    。
  
## <a name="syntax"></a>语法  
  
```  
  
.AsBinaryZM()  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：varbinary(max)   
  
 CLR 返回类型：**SqlBytes**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>示例  
  
```sql  
DECLARE @g1 GEOMETRY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>另请参阅  
 [Geometry 实例上的扩展方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M（geometry 数据类型）](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z（geometry 数据类型）](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  

