---
title: UnionAggregate（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- UnionAggregate
- UnionAggregate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UnionAggregate method (geography)
ms.assetid: 1a3aeef1-5b0e-4ae8-aeb7-c4aab22f42ab
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 02e8ab6517be4a22462bc56c9e6178cd335b7868
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36242999"
---
# <a name="unionaggregate-geography-data-type"></a>UnionAggregate（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

对一组地理对象执行联合操作。
  
## <a name="syntax"></a>语法  
  
```  
  
UnionAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>参数  
 geography_operand  
 geography 类型的表列，其中保存要对其执行联合操作的 geography 对象的集合。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography  
  
## <a name="remarks"></a>Remarks  
 如果输入具有不同的 SRID，方法返回 null。 请参阅[空间引用标识符 (SRID)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)。  
  
 方法忽略 null 输入。  
  
> [!NOTE]  
>  如果所有输入值均为 null，则方法返回 null。  
  
## <a name="examples"></a>示例  
 下面的示例对城市内的一组 geography 位置点执行 `UnionAggregate`。  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::UnionAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态地理方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
