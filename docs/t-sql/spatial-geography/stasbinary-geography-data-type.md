---
title: "STAsBinary (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STAsBinary_TSQL
- STAsBinary (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsBinary method
ms.assetid: 99602a62-265d-4aa4-a8dc-92992ca55ba4
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c48fc48b7af524e980801a11ac2574f2091823a2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stasbinary-geography-data-type"></a>STAsBinary（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回的开放地理空间联盟 (OGC) 熟知二进制 (WKB) 表示形式**geography**实例。  
  
 这**geography**数据类型方法支持**FullGlobe**实例或大于半球的空间实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STAsBinary ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **varbinary （max)**  
  
 CLR 返回类型：**对**  
  
## <a name="remarks"></a>注释  
 OGC 种**geography**实例可以通过调用来确定[STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)。  
  
## <a name="examples"></a>示例  
 下面的示例使用`STAsBinary()`创建`LineString``geography`从实例 （-122.360，47.656） 到 （-122.343，47.656） 从文本。 然后，它以 WKB 的形式返回结果。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING( -122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsBinary();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

