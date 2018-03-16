---
title: "Null（geography 数据类型）| Microsoft Docs"
ms.custom: 
ms.date: 07/30/2017
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
- Null (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Null (geography Data Type)
- Null method
ms.assetid: bb464b06-86e0-4b8b-ad78-04bd33b6069c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0e0b8bd71e8c9ed3066e7d632423162cd165f6a5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="null-geography-data-type"></a>Null（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

提供 **geography** 类型的 Null 实例的只读属性。
  
## <a name="syntax"></a>语法  
  
```  
  
Null  
```  
  
## <a name="arguments"></a>参数  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型：**geography**  
  
 CLR 类型：SqlGeography  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>示例  
 下面的示例检索一个 Null `geography` 实例。  
  
```  
DECLARE @g geography;   
SET @g = geography::[Null];  
SELECT @g  
```  
  
## <a name="see-also"></a>另请参阅  
 [扩展静态地理方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
