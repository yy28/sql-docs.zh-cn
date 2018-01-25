---
title: "M (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- M (geometry Data Type)
- M_TSQL
dev_langs: TSQL
helpviewer_keywords: M (geometry Data Type)
ms.assetid: 443ae2ea-739b-41ef-96cc-ac5dfd65e10b
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39f6677b10632363f91c2572c4a0856a67e436c3
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="m-geometry-data-type"></a>M（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **M** （度量） 值的**几何图形**实例。 度量值的语义是用户定义的。  

## <a name="syntax"></a>语法  
  
```  
  
.M  
```  
  
## <a name="arguments"></a>参数  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型： **float**  
  
 CLR 类型： **SqlDouble**  
  
## <a name="remarks"></a>注释  
 此属性的值为 null 如果**几何图形**实例不是**点**，以及对于任何**点**实例未设置它。  
  
 该属性为只读。  
  
 **M**值不使用任何计算所做的库中，并且将不会传递任何库计算。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个带有 Z（标高）和 M（度量）值的 `Point` 实例，并使用 `M` 获取该实例的 M 值。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>另请参阅  
 [在几何图形实例的扩展的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)   
 [AsTextZM（geometry 数据类型）](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
  

