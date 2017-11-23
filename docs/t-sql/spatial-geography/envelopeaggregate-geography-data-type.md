---
title: "EnvelopeAggregate (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 07/30/2017
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
- EnvelopeAggregate_TSQL
- EnvelopeAggregate
dev_langs: TSQL
helpviewer_keywords: EnvelopeAggregate method (geography)
ms.assetid: 4947797f-edb8-490f-beca-37df9ec06954
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dc24295c305c4cc2ea2e4b6ff5fb3525a315f3d6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="envelopeaggregate-geography-data-type"></a>EnvelopeAggregate（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回给定的一组的边界对象**geography**对象。 生成**geography**对象包含多条圆弧线段。
  
## <a name="syntax"></a>语法  
  
```  
  
EnvelopeAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>参数  
 *geography_operand*  
 是**geography**类型表列包含的一套**geography**对象在其上执行信封聚合操作。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**地理位置**  
  
## <a name="remarks"></a>注释  
 A **FullGlobe**时生成的边界对象大于半球返回对象。 此方法不精确。  
  
 方法返回**null**如果输入具有不同 Srid。 请参阅[空间引用标识符 &#40;Srid &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
 方法将忽略**null**输入。  
  
> [!NOTE]  
>  方法返回**null**如果所有输入的值为**null**。  
  
## <a name="examples"></a>示例  
 下面的示例执行`EnvelopeAggregate`对一组**geography**位置内城市的点。  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::EnvelopeAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态地理方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
