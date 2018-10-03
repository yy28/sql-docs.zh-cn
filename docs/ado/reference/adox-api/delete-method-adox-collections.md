---
title: Delete 方法 （ADOX 集合） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90f9aa6a788296ff5fef05e96b7f46b56729ded9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811075"
---
# <a name="delete-method-adox-collections"></a>Delete 方法（ADOX 集合）
从集合中删除的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
 一个**变体**指定名称或序号位置 （索引） 的要删除的对象。  
  
## <a name="remarks"></a>备注  
 如果将会出错*名称*集合中不存在。  
  
 有关[表](../../../ado/reference/adox-api/tables-collection-adox.md)并[用户](../../../ado/reference/adox-api/users-collection-adox.md)集合，如果将发生错误的提供程序不支持删除表或用户，分别。 有关[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)并[视图](../../../ado/reference/adox-api/views-collection-adox.md)集合**删除**如果提供程序不支持保留命令将失败。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[列集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[组集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[项集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[过程集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|[表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[用户集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>请参阅  
 [过程 Delete 方法示例 (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [视图 Delete 方法示例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
