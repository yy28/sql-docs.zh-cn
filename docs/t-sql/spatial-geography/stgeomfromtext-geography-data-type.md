---
title: STGeomFromText（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomFromText (geography Data Type)
- STGeomFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full globe
- STGeomFromText method
ms.assetid: 3717987b-77d8-4ccf-a1db-5a8016ac1083
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 90359259bb7ba85377e72c40a8eece79de44cbf2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68042120"
---
# <a name="stgeomfromtext-geography-data-type"></a>STGeomFromText（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

从开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式返回 geography 实例，增加了该实例传递的任何 Z（标高）和 M（度量）值  。
  
这种 geography 数据类型方法支持大于半球的 FullGlobe 实例或空间实例   。
  
## <a name="syntax"></a>语法  
  
```  
  
STGeomFromText ( 'geography_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 geography_tagged_text   
 要返回的 geography 实例的 WKT 表示形式  。 geography_tagged_text 是一个 nvarchar(max) 表达式   。  
  
 SRID   
 一个 int 表达式，表示要返回的 geography 实例的空间引用 ID (SRID)   。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography   
  
 CLR 返回类型：SqlGeography   
  
## <a name="remarks"></a>备注  
 STGeomFromText() 返回的 **geography** 实例的 OGC 类型设置为相应的 WKT 输入。  
  
 如果输入包含对跖边缘，此方法将引发 **ArgumentException**。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STGeomFromText()` 创建 `geography` 实例。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态地理方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
