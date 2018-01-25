---
title: "STAsText (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- STAsText (geography Data Type)
- STAsText_TSQL
dev_langs: TSQL
helpviewer_keywords: STAsText method
ms.assetid: d3d2635d-ca6c-4205-9d6c-eb939ee314fd
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c41abc14564547efa56be18cb1fa18bfa0443f2e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stastext-geography-data-type"></a>STAsText（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回的开放地理空间联盟 (OGC) 熟知文本 (WKT) 表示形式**geography**实例。 此文本将不包含该实例传递的任何 Z（标高）或 M（度量）值。  
  
 这**geography**数据类型方法支持**FullGlobe**实例或大于半球的空间实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STAsText ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **nvarchar (max)**  
  
 CLR 返回类型：**对**  
  
## <a name="remarks"></a>注释  
 OGC 种**geography**实例可以通过调用来确定[STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)。  
  
 在[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，可能返回的结果集在服务器上已扩展到**FullGlobe**实例。  
  
## <a name="examples"></a>示例  
 下面的示例使用`STAsText()`创建`LineString``geography`从实例 （-122.360，47.656） 到 （-122.343，47.656） 从文本。 然后，它以文本的形式返回结果。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
