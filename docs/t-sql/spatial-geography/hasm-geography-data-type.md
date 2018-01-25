---
title: "HasM (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 05/04/2017
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
- HasM_TSQL
- HasM
dev_langs: TSQL
helpviewer_keywords: HasM geography
ms.assetid: e752e97f-1619-437d-b962-48c188b4e94c
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bad79780c74f3fe512eb394c7fc997d962594e12
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="hasm-geography-data-type"></a>HasM （geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果空间对象包含至少一个 M 值，则返回 1 (true)；否则返回 0 (false)。  
  
## <a name="syntax"></a>语法  
  
```  
  
.HasM  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型：**布尔**  
  
## <a name="remarks"></a>注释  
  
## <a name="examples"></a>示例  
  
```sql  
DECLARE @p GEOGRAPHY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例的扩展的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [&#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/m-geography-data-type.md)  
  
  
