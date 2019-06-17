---
title: Append 方法 （ADOX 组） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b6b9740b58ef53fd4fcc2becda50f73609a1bf5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708361"
---
# <a name="append-method-adox-groups"></a>Append 方法（ADOX 组）
添加一个新[组](../../../ado/reference/adox-api/group-object-adox.md)对象传递给[组](../../../ado/reference/adox-api/groups-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>Parameters  
 *分组*  
 **组**对象以追加或要创建并追加的组的名称。  
  
## <a name="remarks"></a>备注  
 **组**系列[目录](../../../ado/reference/adox-api/catalog-object-adox.md)表示所有目录的组帐户。 **组**集合[用户](../../../ado/reference/adox-api/user-object-adox.md)表示只有该用户所属的组。  
  
 如果提供程序不支持创建组，将会出错。  
  
> [!NOTE]
>  之前追加**组**对象传递给**组**的集合**用户**对象，**组**对象具有相同[名称](../../../ado/reference/adox-api/name-property-adox.md)如要追加的一个必须已存在于**组**的集合**目录**。  
  
## <a name="applies-to"></a>适用范围  
 [组集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>请参阅  
 [组和用户 Append、 ChangePassword 方法示例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 方法 （ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 项）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 （ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
