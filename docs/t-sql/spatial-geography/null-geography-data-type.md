---
title: "Null (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Null (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Null (geography Data Type)
- Null method
ms.assetid: bb464b06-86e0-4b8b-ad78-04bd33b6069c
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 48df84157bf4b54c45c734cdc9338a95fc1b13ab
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="null-geography-data-type"></a>Null（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

提供的 null 实例的只读属性**geography**类型。
  
## <a name="syntax"></a>语法  
  
```  
  
Null  
```  
  
## <a name="arguments"></a>参数  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型：**地理位置**  
  
 CLR 类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
  
## <a name="examples"></a>示例  
 下面的示例检索一个 Null `geography` 实例。  
  
```  
DECLARE @g geography;   
SET @g = geography::[Null];  
SELECT @g  
```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态 Geography 方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

