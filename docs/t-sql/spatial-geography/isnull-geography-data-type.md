---
title: "IsNull (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IsNull (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c07ddb41209c507845da7e790035ab54ed1044f1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="isnull-geography-data-type"></a>IsNull（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  一个属性，指定如果**geography**实例为 null。 如果实例为 Null，则返回“TRUE”；如果实例不为 Null，则返回 0。  
  
## <a name="syntax"></a>语法  
  
```  
  
.IsNull  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型：**位**  
  
 CLR 类型： **SqlBoolean**  
  
## <a name="remarks"></a>注释  
 `IsNull`可以用于测试是否**geography**实例为 null。 这会产生有些令人混淆的结果：如果实例不为 Null，则返回 0，但是如果实例为 Null 则返回 Null。  
  
 此方法主要由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]基础结构; 建议使用 T-SQL 的谓词 IS NULL 测试是否**geography**实例为 null。 有关详细信息的 T-SQL 谓词 IS NULL，请参阅[IS NULL &#40;Transact SQL &#41;](../../t-sql/queries/is-null-transact-sql.md).  
  
## <a name="examples"></a>示例  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
