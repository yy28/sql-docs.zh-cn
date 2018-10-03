---
title: Null（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Null (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Null (geography Data Type)
- Null method
ms.assetid: bb464b06-86e0-4b8b-ad78-04bd33b6069c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4972ec118bf7d9abc146271c97072a7184d726af
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720165"
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
  
  
