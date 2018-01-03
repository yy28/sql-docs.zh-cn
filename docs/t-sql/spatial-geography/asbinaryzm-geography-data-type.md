---
title: "AsBinaryZM (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- AsBinaryZM
- AsBinaryZM_TSQL
dev_langs: TSQL
helpviewer_keywords:
- AsBinaryZM, geography
- AsBinaryZM
ms.assetid: 37246adb-814d-4113-9983-4d336de8182c
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9abdf15e501c014a53c587799c6f246113567cb9
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="asbinaryzm-geography-data-type"></a>AsBinaryZM（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回的开放地理空间联盟 (OGC) 熟知二进制 (WKB) 表示形式**几何图形**实例扩充与任意**Z** （仰角） 和**M** （度量值）实例传送的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
.AsBinaryZM()  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **varbinary （max)**  
  
 CLR 返回类型：**对**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>示例  
  
```sql  
DECLARE @g1 GEOGRAPHY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例的扩展的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [&#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40; geography 数据类型 &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
