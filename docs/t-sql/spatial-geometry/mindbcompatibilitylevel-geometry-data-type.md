---
title: MinDbCompatibilityLevel（geometry 数据类型）| Microsoft Docs
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
- MinDbCompatibilityLevel method (geometry)
ms.assetid: c848b974-8ccb-4c5c-a7eb-b019a9538d99
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: ea7e2309518a414f662581ac1f5db95976ecaf8b
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937518"
---
# <a name="mindbcompatibilitylevel-geometry-data-type"></a>MinDbCompatibilityLevel（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回识别 geometry 数据类型实例的最基本的数据库兼容级别。
  
## <a name="syntax"></a>语法  
  
```  
  
.MinDbCompatibilityLevel ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：int  
  
 CLR 返回类型：int  
  
## <a name="remarks"></a>Remarks  
 在更改数据库的兼容级别之前应使用 `MinDbCompatibilityLevel()` 测试空间对象的兼容性。  
  
## <a name="examples"></a>示例  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>A. 在兼容级别为 110 的情况下测试 CircularString 类型是否兼容  
 下面的示例测试 `CircularString` 实例是否与较早版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 兼容：  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(3 4, 8 9, 5 6)'; 
 IF @g.MinDbCompatibilityLevel() <= 110 
 BEGIN 
 SELECT @g.ToString(); 
 END
 ```  
  
### <a name="b-testing-linestring-type-for-compatibility-with-compatibility-level-100"></a>B. 在兼容级别为 100 的情况下测试 LineString 类型是否兼容  
 下面的示例测试 `LineString` 实例是否与 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 兼容：  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 9, 5 6)'; 
 IF @g.MinDbCompatibilityLevel() <= 100 
 BEGIN 
 SELECT @g.ToString(); 
 END
``` 
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE 兼容级别 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

