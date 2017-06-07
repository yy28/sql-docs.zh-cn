---
title: "在 JSON 中添加 NULL 值 - INCLUDE_NULL_VALUES 选项 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- INCLUDE_NULL_VALUES (FOR JSON)
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 04389191586bf45a45a1771781858ec31e6f988a
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="include-null-values-in-json---includenullvalues-option"></a>在 JSON 中添加 NULL 值 - INCLUDE_NULL_VALUES 选项
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  若要在 **FOR JSON** 子句的 JSON 输出中添加 NULL 值，请指定 **INCLUDE_NULL_VALUES** 选项。  
  
 如果你没有指定 **INCLUDE_NULL_VALUES** 选项，则 JSON 输出不会包括查询结果中 NULL 值所对应的属性。  
  
## <a name="examples"></a>示例  
 以下示例介绍了在指定和未指定 **INCLUDE_NULL_VALUES** 选项的情况下 **FOR JSON** 子句的输出。  
  
|未指定 **INCLUDE_NULL_VALUES** 选项|已指定 **INCLUDE_NULL_VALUES** 选项|  
|--------------------------------------------------|-----------------------------------------------|  
|`{    "name": "John",    "surname": "Doe" }`|`{    "name": "John",    "surname": "Doe",    "age": null,    "phone": null }`|  
  
 下面又通过一个示例介绍了在指定 **INCLUDE_NULL_VALUES** 选项的情况下 **FOR JSON** 子句的输出。  
  
 **Query**  
  
```sql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO, INCLUDE_NULL_VALUES    
```  
  
 **结果**  
  
```json  
[{
    "name": "John",
    "surname": null
}, {
    "name": "Jane",
    "surname": "Doe"
}] 
```  
  
## <a name="see-also"></a>另请参阅  
 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

