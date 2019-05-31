---
title: STGeomFromWKB（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomFromWKB_TSQL
- STGeomFromWKB (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomFromWKB method
ms.assetid: 79d39d88-5440-49a7-9247-190eafce3f4f
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: d0ca85d39df85fc48a9aad779414db1dcc1b4de6
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2019
ms.locfileid: "65936912"
---
# <a name="stgeomfromwkb-geography-data-type"></a>STGeomFromWKB（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

从开放地理空间信息联盟 (OGC) 已知二进制 (WKB) 表示形式中返回 geography 实例  。
  
这种 geography 数据类型方法支持大于半球的 FullGlobe 实例或空间实例   。
  
## <a name="syntax"></a>语法  
  
```  
  
STGeomFromWKB ( 'WKB_geography' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 WKB_geography   
 要返回的 geography  实例的 WKB 表示形式。 WKB_geography 是一种 varbinary(max) 表达式   。  
  
 SRID   
 一个 int 表达式，表示要返回的 geography 实例的空间引用 ID (SRID)   。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography   
  
 CLR 返回类型：**SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 `STGeomFromText()` 返回的 geography  实例的 OGC 类型设置为相应的 WKB 输入。  
  
 如果输入的格式不正确，此方法将引发 FormatException  。  
  
 如果输入包含对跖边缘，此方法将引发 ArgumentException  。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STGeomFromWKB()` 创建 `geography` 实例。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromWKB(0x010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态地理方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
