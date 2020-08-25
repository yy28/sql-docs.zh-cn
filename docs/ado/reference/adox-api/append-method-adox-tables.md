---
description: Append 方法（ADOX 表）
title: )  (ADOX 表的 Append 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Tables::Append
- Tables::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: a362ed51-314c-4783-9598-538dbf755f3d
author: rothja
ms.author: jroth
ms.openlocfilehash: 2f54f1491327b9b0294dec1332a3fb9ff8b2c69c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771386"
---
# <a name="append-method-adox-tables"></a>Append 方法（ADOX 表）
向[Tables](./tables-collection-adox.md)集合添加一个新的[Table](./table-object-adox.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Tables.Append Table  
```  
  
#### <a name="parameters"></a>parameters  
 *表*  
 一个包含对要追加的**表**的引用的**变量**值，或者是要创建并追加的表的名称。  
  
## <a name="remarks"></a>备注  
 如果提供程序不支持创建表，则会发生错误。  
  
## <a name="applies-to"></a>适用于  
 [表集合 (ADOX)](./tables-collection-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [列和表追加方法、Name 属性示例 (VB) ](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [ParentCatalog 属性示例 (VB) ](./parentcatalog-property-example-vb.md)   
 [Append 列 (追加方法) ](./append-method-adox-columns.md)   
 [将方法追加 (ADOX 组) ](./append-method-adox-groups.md)   
 [Append 索引 (Append 方法) ](./append-method-adox-indexes.md)   
 [追加方法 (ADOX 密钥) ](./append-method-adox-keys.md)   
 [附加方法 (ADOX 过程) ](./append-method-adox-procedures.md)   
 [ADOX 用户 (追加方法) ](./append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](./append-method-adox-views.md)