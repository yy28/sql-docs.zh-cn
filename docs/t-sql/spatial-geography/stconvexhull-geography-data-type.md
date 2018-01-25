---
title: "STConvexHull (geography 数据类型) |Microsoft 文档"
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
dev_langs: TSQL
helpviewer_keywords: STConvexHull method (geography)
ms.assetid: fb435db7-31bb-4243-9d8b-35379184cfb4
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d797c6e2b0e4f7163aae0e1b6ecb37af95051942
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="stconvexhull-geography-data-type"></a>STConvexHull（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回一个对象，表示的凸包**geography**实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
 CLR 返回类型： **SqlGeography**  
  
## <a name="remarks"></a>注释  
 返回`FullGlobe`对象**geography**实例具有大于 90 度的信封角度。  
  
 返回一个空**geography**为一个空集合**geography**实例。  
  
 返回**null**为未初始化**geography**实例。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-stconvexhull-on-an-uninitialized-geography-instance"></a>A. 对未初始化的 geography 实例使用 STConvexHull()  
 下面的示例使用`STConvexHull()`对未初始化**geography**实例。  
  
```
 DECLARE @g geography;  
 SELECT @g.STConvexHull();
 ```  
  
### <a name="b-using-stconvexhull-on-an-empty-geography-instance"></a>B. 对空的 geography 实例使用 STConvexHull  
 以下示例对空的 `STConvexHull()` 实例使用 `Polygon`。  
  
```
 DECLARE @g geography = 'POLYGON EMPTY';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
### <a name="c-finding-the-convex-hull-of-a-non-convex-polygon-instance"></a>C. 查找非凸 Polygon 实例的凸包  
 下面的示例使用 `STConvexHull()` 查找非凸 `Polygon` 实例的凸包。  
  
```  
 DECLARE @g geography;  
 SET @g = geography::Parse('POLYGON((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
 SELECT @g.STConvexHull().ToString();  
```  
  
### <a name="d-finding-the-convex-hull-on-a-geography-instance-with-an-envelope-angle-larger-than-90-degrees"></a>D. 在一个信封角大于 90 度的 geography 实例上查找凸包  
 下面的示例使用`STConvexHull()`上**geography**信封角度大于 90 度的实例。  
  
```
 DECLARE @g geography = 'POLYGON((20.533 46.566, -18.283 46.1, -22.3 47.45, 20.533 46.566))';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
  
