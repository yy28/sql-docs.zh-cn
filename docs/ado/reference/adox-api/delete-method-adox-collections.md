---
title: Delete 方法（ADOX 集合） |Microsoft Docs
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
ms.openlocfilehash: be2aa91cf27d7dc12d3cd0c1e0bf719bd43797ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966430"
---
# <a name="delete-method-adox-collections"></a>Delete 方法（ADOX 集合）
从集合中删除对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>parameters  
 *名称*  
 一个**变量**，它指定要删除的对象的名称或序号位置（索引）。  
  
## <a name="remarks"></a>备注  
 如果集合中不存在该*名称*，则会发生错误。  
  
 对于[表](../../../ado/reference/adox-api/tables-collection-adox.md)和[用户](../../../ado/reference/adox-api/users-collection-adox.md)集合，如果提供程序不支持删除表或用户，则会发生错误。 对于 "过程" 和 "[视图](../../../ado/reference/adox-api/views-collection-adox.md)" 集合，如果提供程序不支持保留命令，则**删除**[操作](../../../ado/reference/adox-api/procedures-collection-adox.md)将失败。  
  
## <a name="applies-to"></a>应用于  
  
||||  
|-|-|-|  
|[列集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[组集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[项集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[过程集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|[表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[用户集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>另请参阅  
 [过程 Delete 方法示例（VB）](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [视图 Delete 方法示例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
