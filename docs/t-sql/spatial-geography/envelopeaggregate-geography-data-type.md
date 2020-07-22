---
title: EnvelopeAggregate（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeAggregate_TSQL
- EnvelopeAggregate
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAggregate method (geography)
ms.assetid: 4947797f-edb8-490f-beca-37df9ec06954
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5e90ae8b7716c3ede90a2a80f5c904f0d02216a5
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555441"
---
# <a name="envelopeaggregate-geography-data-type"></a>EnvelopeAggregate（geography 数据类型）
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

为一组给定的 geography 对象返回边界对象  。 所生成的 geography 对象包含多个圆弧段  。
  
## <a name="syntax"></a>语法  
  
```  
  
EnvelopeAggregate ( geography_operand )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>参数
 geography_operand   
 geography 类型的表列，其中保存要对其执行包络线聚合操作的 geography 对象的集合   。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography   
  
## <a name="remarks"></a>备注  
 当产生的边界对象大于半球时，将返回 FullGlobe 对象  。 此方法不精确。  
  
 如果输入具有不同的 SRID，方法返回 null  。 请参阅[空间引用标识符 (SRID)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)。  
  
 方法忽略 null 输入  。  
  
> [!NOTE]  
>  如果所有输入值均为 null，则方法返回 null   。  
  
## <a name="examples"></a>示例  
 下面的示例对城市内的一组 geography 位置点执行 `EnvelopeAggregate`  。  
  
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
  
  
