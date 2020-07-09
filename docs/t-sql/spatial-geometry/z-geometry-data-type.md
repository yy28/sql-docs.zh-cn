---
title: Z（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Z (geometry Data Type)
- Z_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Z (geometry Data Type)
ms.assetid: a62ed736-44df-4591-9109-ce90e1df9bd3
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 40afdb720e125899e8a4c3b7df942496b7d0ae44
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762068"
---
# <a name="z-geometry-data-type"></a>Z（geometry 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

实例的 Z（标高）值。 标高值的语义是用户定义的。
  
## <a name="syntax"></a>语法  
  
```  
  
.Z  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型：float   
  
 CLR 类型：SqlDouble   
  
## <a name="remarks"></a>备注  
 如果 geometry 实例不是 point，则此属性的值为 null；对于未设置此属性的任何 **Point** 实例，此属性的值也为 null。  
  
 此属性为只读。  
  
 Z 坐标未在库进行的任何计算中使用，因此不通过任何库计算传递。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个带有 Z（标高）和 M（度量）值的 `Point` 实例，并使用 `Z` 获取该实例的 Z 值。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>另请参阅  
 [M（geometry 数据类型）](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [AsTextZM（geometry 数据类型）](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)   
 [几何图形实例上的扩展方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

