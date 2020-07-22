---
title: HasZ（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HasZ
- HasZ_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- HasZ geography
ms.assetid: 4c5e1669-a987-4dda-9ebf-f573ce615c34
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e8717241af662ddf199cba189cdfe5449d1962db
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555417"
---
# <a name="hasz-geography-data-type"></a>HasZ（geography 数据类型）
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  如果空间对象包含至少一个 Z 值，则返回 1 (true)；否则返回 0 (false)。  
  
## <a name="syntax"></a>语法  
  
```  
  
.HasZ  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>返回类型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：bit   
  
 CLR 返回类型：Boolean   
  
## <a name="remarks"></a>备注  
  
## <a name="examples"></a>示例  
  
```sql  
DECLARE @p GEOGRAPHY = 'Point(1 1 1 1)'  
SELECT @p.HasZ   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>另请参阅  
 [Geography 实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Z（geography 数据类型）](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
