---
title: "AsTextZM (geography 数据类型) |Microsoft 文档"
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
- AsTextZM (geography Data Type)
- AsTextZM_TSQL
- AsTextZM
- AsTextZM_(geography_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM method
ms.assetid: e9dc27f6-e945-4457-8498-7644db34008e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ba824c4482f49d534d11666054a0a8d3a1669d2d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="astextzm-geography-data-type"></a>AsTextZM（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回的开放地理空间联盟 (OGC) 熟知文本 (WKT) 表示形式**geography**实例扩充与任意**Z** （仰角） 和**M** （度量值）实例传送的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **nvarchar (max)**  
  
 CLR 返回类型：**对**  
  
## <a name="remarks"></a>注释  
  
## <a name="examples"></a>示例  
 下面的示例创建`Point`实例，其中包含**Z** （仰角） 和**M** （度量） 值。 `STAsText()`选择 WKT 值，(-122.34900 47.65100);`AsTextZM()`选择相同的 WKT 值，并返回的值**Z**和**M**、 生成 (-122.34900 47.65100 10.3 12)。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例的扩展的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [&#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  

