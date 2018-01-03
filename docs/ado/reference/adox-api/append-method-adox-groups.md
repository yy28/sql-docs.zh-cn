---
title: "Append 方法 （ADOX 组） |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords: Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e9f1d71811195f214bc3c25db73dee21779f2b6e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="append-method-adox-groups"></a>Append 方法 （ADOX 组）
添加新[组](../../../ado/reference/adox-api/group-object-adox.md)对象传递给[组](../../../ado/reference/adox-api/groups-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>Parameters  
 *分组*  
 **组**要追加的对象或组要创建并追加的名称。  
  
## <a name="remarks"></a>Remarks  
 **组**集合[目录](../../../ado/reference/adox-api/catalog-object-adox.md)表示所有目录的组帐户。 **组**集合[用户](../../../ado/reference/adox-api/user-object-adox.md)表示仅用户所属的组。  
  
 如果提供程序不支持创建组，将会出错。  
  
> [!NOTE]
>  在追加之前**组**对象传递给**组**集合**用户**对象，**组**对象具有相同[名称](../../../ado/reference/adox-api/name-property-adox.md)如要追加的一个必须已存在于**组**集合**目录**。  
  
## <a name="applies-to"></a>适用范围  
 [组集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [组和用户追加，ChangePassword 方法示例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 方法 （ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 键）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 （ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
