---
title: IsNull（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsNull (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull (geometry Data Type)
ms.assetid: f95813a5-26c0-48aa-bfb8-56d2a0980788
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 89bbf3581f8a62750338d1d7ea360fc46ea36479
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682023"
---
# <a name="isnull-geometry-data-type"></a>IsNull（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

geometry 实例的类型为 Null。 如果该实例不为 Null，则返回 0。
  
## <a name="syntax"></a>语法  
  
```  
.IsNull  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型：bit  
  
 CLR 类型：SqlBoolean  
  
## <a name="remarks"></a>Remarks  
 `IsNull` 可用于测试 geometry 实例是否为 Null。 这会产生有些令人混淆的结果：如果实例不为 Null，则返回 0，但是如果实例为 Null 则返回 Null。  
  
 此方法主要供 SQL Server 基础结构使用；建议您不要使用 `IsNull` 来测试实例是否为 Null。  
  

## <a name="see-also"></a>另请参阅  
 [几何图形实例上的扩展方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

