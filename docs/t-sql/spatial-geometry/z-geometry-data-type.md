---
title: "Z (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Z (geometry Data Type)
- Z_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Z (geometry Data Type)
ms.assetid: a62ed736-44df-4591-9109-ce90e1df9bd3
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad6d857cb2028c34e6c1d1e9200537fbcd007989
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="z-geometry-data-type"></a>Z（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

实例的 Z（标高）值。 标高值的语义是用户定义的。
  
## <a name="syntax"></a>语法  
  
```  
  
.Z  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型： **float**  
  
 CLR 类型： **SqlDouble**  
  
## <a name="remarks"></a>注释  
 此属性的值将为 null 的几何图形实例不是一个点，以及如果对待任何**点**实例未设置它。  
  
 该属性为只读。  
  
 Z 坐标不使用任何计算所做的库中，并且不会传递任何库计算。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个带有 Z（标高）和 M（度量）值的 `Point` 实例，并使用 `Z` 获取该实例的 Z 值。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [AsTextZM &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)   
 [在几何图形实例的扩展的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


