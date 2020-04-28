---
title: Append 方法（ADOX 组） |Microsoft Docs
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
ms.openlocfilehash: 8281b8b480289dca2b4976cea61a6d6838fa2779
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967314"
---
# <a name="append-method-adox-groups"></a>Append 方法（ADOX 组）
向[Groups](../../../ado/reference/adox-api/groups-collection-adox.md)集合添加一个新的[组](../../../ado/reference/adox-api/group-object-adox.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>参数  
 *组*  
 要追加的**组**对象或要创建和追加的组的名称。  
  
## <a name="remarks"></a>备注  
 [目录](../../../ado/reference/adox-api/catalog-object-adox.md)的**Groups**集合表示所有目录的组帐户。 [用户](../../../ado/reference/adox-api/user-object-adox.md)的**Groups**集合仅表示该用户所属的组。  
  
 如果提供程序不支持创建组，将出现错误。  
  
> [!NOTE]
>  在将**组**对象追加到**用户**对象的**groups**集合之前，**目录**的**组**集合中必须已经存在与要追加的组[对象同名的](../../../ado/reference/adox-api/name-property-adox.md)**组**对象。  
  
## <a name="applies-to"></a>应用于  
 [组集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [组和用户追加，ChangePassword 方法示例（VB）](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 方法（ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法（ADOX 键）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法（ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法（ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法（ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
