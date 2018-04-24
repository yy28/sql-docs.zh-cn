---
title: IsNull（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IsNull (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f2bfa2b771d02649f40e2e7b93a61777bfd38da8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="isnull-geography-data-type"></a>IsNull（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定 geography 实例是否为 Null 的属性。 如果实例为 Null，则返回“TRUE”；如果实例不为 Null，则返回 0。  
  
## <a name="syntax"></a>语法  
  
```  
  
.IsNull  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型：bit  
  
 CLR 类型：SqlBoolean  
  
## <a name="remarks"></a>Remarks  
 `IsNull` 可用于测试 geography 实例是否为 Null。 这会产生有些令人混淆的结果：如果实例不为 Null，则返回 0，但是如果实例为 Null 则返回 Null。  
  
 此方法主要供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基础结构使用；建议使用 T-SQL 谓词 IS NULL 来测试 geography 实例是否为 Null。 有关 T-SQL 谓词 IS NULL 的详细信息，请参阅 [IS NULL (Transact-SQL)](../../t-sql/queries/is-null-transact-sql.md)。  
  
## <a name="examples"></a>示例  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
