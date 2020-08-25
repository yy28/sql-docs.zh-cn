---
description: ADOX 对象
title: ADOX 对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- objects [ADOX]
- ADOX, objects
ms.assetid: 3f5287e9-f62c-40c4-bb59-985102be956e
author: rothja
ms.author: jroth
ms.openlocfilehash: ca5131235b4c34c05f4cc3b783087f25dc027e95
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771576"
---
# <a name="adox-objects"></a>ADOX 对象
## <a name="adox-object-summary"></a>ADOX 对象摘要  
  
|对象|说明|  
|------------|-----------------|  
|[目录](./catalog-object-adox.md)|包含描述数据源的架构目录的集合。|  
|[列](./column-object-adox.md)|表示表、索引或键中的列。|  
|[组](./group-object-adox.md)|表示在受保护的数据库中具有访问权限的组帐户。|  
|[Index](./index-object-adox.md)|表示数据库表中的索引。|  
|[Key](./key-object-adox.md)|表示数据库表中的主键或唯一键字段。|  
|[方法](./procedure-object-adox.md)|表示存储过程。|  
|[表](./table-object-adox.md)|表示数据库表，其中包括列、索引和键。|  
|[用户](./user-object-adox.md)|表示在受保护的数据库中具有访问权限的用户帐户。|  
|[视图](./view-object-adox.md)|表示一组筛选的记录或虚拟表。|  
  
 [ADOX 对象模型](./adox-object-model.md)中阐释了这些对象之间的关系。  
  
 每个对象都可以包含在其对应的集合中。 例如， **表** 对象可以包含在 [表](./tables-collection-adox.md) 集合中。 有关详细信息，请参阅 [ADOX 集合](./adox-collections.md) 或特定集合主题。  
  
## <a name="see-also"></a>另请参阅  
 [ADOX API 参考](./adox-object-model.md?view=sql-server-ver15)   
 [ADOX 集合](./adox-collections.md)   
 [ADOX 对象模型](./adox-object-model.md)   
 [数据定义语言和安全性的 ADO 扩展 (ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)