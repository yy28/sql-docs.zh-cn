---
title: STOverlaps（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STOverlaps method (geography)
ms.assetid: 2babbb9c-59ef-4494-9e6b-528cf296cbd7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: fc0d0a449941c3d8a04526180cfa721931d98d09
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68120845"
---
# <a name="stoverlaps-geography-data-type"></a>STOverlaps（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  如果 geography 实例在空间上与另一个 geography 实例重叠，则返回 1；否则，返回 0   。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STOverlaps ( other_geography )  
```  
  
## <a name="arguments"></a>参数  
 other_geography   
 与对其调用 `STOverlaps()` 的实例进行比较的其他 geography 实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：bit   
  
 CLR 返回类型：SqlBoolean   
  
## <a name="remarks"></a>备注  
 如果 geography 实例的空间引用 ID (SRID) 不匹配，则此方法始终返回 null  。  
  
## <a name="examples"></a>示例  
 以下示例使用 `STOverlaps()` 测试两个 geography 实例是否重叠  。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::Parse('POLYGON ((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
SET @h = geography::Parse('CURVEPOLYGON (COMPOUNDCURVE (CIRCULARSTRING (-122.200928 47.454094, -122.810669 47.00648, -122.942505 46.687131, -121.14624 45.786679, -119.119263 46.183634), (-119.119263 46.183634, -119.273071 47.107523), CIRCULARSTRING (-119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)))');  
SELECT @g.STOverlaps(@h);  
```  
  
  
