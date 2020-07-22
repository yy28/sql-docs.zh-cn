---
title: Null（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Null (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Null (geometry Data Type)
ms.assetid: 67a4b019-9091-4443-85cc-f4836d0cb509
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9e93cb4a8e079d54098ff0a7c466de0227965487
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555092"
---
# <a name="null-geometry-data-type"></a>Null（geometry 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

提供 **geometry** 类型的 Null 实例的只读属性。
  
## <a name="syntax"></a>语法  
  
```  
  
Null  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>参数
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型：**geometry**  
  
 CLR 类型：**SqlGeometry**  
  
## <a name="remarks"></a>备注  
  
## <a name="examples"></a>示例  
 下面的示例检索一个 Null `geometry` 实例。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::[Null];  
SELECT @g  
```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态几何图形方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

