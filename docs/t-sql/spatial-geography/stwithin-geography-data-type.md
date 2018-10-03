---
title: STWithin（geography 数据类型）| Microsoft Docs
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
- STWithin method (geography)
ms.assetid: 6fc745cc-7976-418a-a89a-c267e64ab3a2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 93715075a2313a53c6b7221deb6a10758e35cf8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47712455"
---
# <a name="stwithin-geography-data-type"></a>STWithin（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果 geography 实例在空间上包含在另一个 geography 实例中，则返回 1；否则，返回 0。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STWithin ( other_geography )  
```  
  
## <a name="arguments"></a>参数  
 other_geography  
 与对其调用 `STWithin()` 的实例进行比较的其他 geography 实例。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：bit  
  
 CLR 返回类型：SqlBoolean  
  
## <a name="remarks"></a>Remarks  
 如果 geography 实例的空间引用 ID (SRID) 不匹配，则此方法始终返回 null。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STWithin()` 来测试两个 `geography` 实例，以查看第一个实例是否完全包含在第二个实例中。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::Parse('POLYGON ((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
SET @h = geography::Parse('CURVEPOLYGON (COMPOUNDCURVE (CIRCULARSTRING (-122.200928 47.454094, -122.810669 47.00648, -122.942505 46.687131, -121.14624 45.786679, -119.119263 46.183634), (-119.119263 46.183634, -119.273071 47.107523), CIRCULARSTRING (-119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)))');  
SELECT @g.STWithin(@h);  
```  
  
  
