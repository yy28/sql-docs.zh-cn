---
description: Delete 方法（ADOX 集合）
title: 删除方法 (ADOX 集合) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::Delete
- Groups::Delete
- Indexes::raw_Delete
- Columns::raw_Delete
- Tables::Delete
- Keys::Delete
- Users::Delete
- Users::raw_Delete
- Keys::raw_Delete
- Procedures::raw_Delete
- Views::raw_Delete
- Indexes::Delete
- Procedures::Delete
- Groups::raw_Delete
- Tables::raw_Delete
- Columns::Delete
helpviewer_keywords:
- delete method [ADOX]
ms.assetid: e6b6e3a4-8952-4d79-81f4-51019c338374
author: rothja
ms.author: jroth
ms.openlocfilehash: 7345337ab35f4154fd9dc53f749e04dba96dad48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440109"
---
# <a name="delete-method-adox-collections"></a>Delete 方法（ADOX 集合）
从集合中删除对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>参数  
 *名称*  
 一个 **变量** ，指定要删除的对象 (索引) 的名称或序号位置。  
  
## <a name="remarks"></a>备注  
 如果集合中不存在该 *名称* ，则会发生错误。  
  
 对于 [表](../../../ado/reference/adox-api/tables-collection-adox.md) 和 [用户](../../../ado/reference/adox-api/users-collection-adox.md) 集合，如果提供程序不支持删除表或用户，则会发生错误。 对于 "过程" 和 "[视图](../../../ado/reference/adox-api/views-collection-adox.md)" 集合，如果提供程序不支持保留命令，则**删除**[操作](../../../ado/reference/adox-api/procedures-collection-adox.md)将失败。  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [列集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
        [组集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
        [索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
    :::column-end:::
    :::column:::
        [项集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
        [过程集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
        [表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)  
    :::column-end:::
    :::column:::
        [用户集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
        [视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [过程 Delete 方法示例 (VB) ](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [视图 Delete 方法示例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
