---
title: "AsBinaryZM (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- AsBinaryZM geometry
ms.assetid: 5eae2872-adca-4b8f-8b04-4ee91ced98f1
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d7f3c44fe978f6b6d28861a167cbe586577afb3
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="asbinaryzm-geometry-datatype"></a>AsBinaryZM（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回的开放地理空间联盟 (OGC) 熟知二进制 (WKB) 表示形式**几何图形**实例扩充与任意**Z** （仰角） 和**M** （度量值）实例传送的值。
  
## <a name="syntax"></a>语法  
  
```  
  
.AsBinaryZM()  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **varbinary （max)**  
  
 CLR 返回类型：**对**  
  
## <a name="remarks"></a>注释  
  
## <a name="examples"></a>示例  
  
```sql  
DECLARE @g1 GEOMETRY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>另请参阅  
 [在几何图形实例的扩展的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [&#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  

