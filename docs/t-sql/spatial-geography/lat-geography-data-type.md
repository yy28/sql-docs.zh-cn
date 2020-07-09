---
title: Lat（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Lat
- Lat_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Lat method
ms.assetid: 051d66bc-04de-4c58-861c-760dc5b859b5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 13480e616b9c405e6b740d1632f62827cb33a3e2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731107"
---
# <a name="lat-geography-data-type"></a>Lat（geography 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  geography 实例的纬度属性  。  
  
## <a name="syntax"></a>语法  
  
```  
.Lat  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型：float   
  
 CLR 类型：SqlDouble   
  
## <a name="remarks"></a>备注  
 在 OpenGIS 模型中，仅对由一个点组成的 geography 实例定义 Lat  。 如果 geography 实例包含多个点，则此属性返回 NULL  。 此属性是精确属性，且是只读的。  
  
## <a name="examples"></a>示例  
 此示例创建一个点并返回该点的纬度。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Lat;  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
