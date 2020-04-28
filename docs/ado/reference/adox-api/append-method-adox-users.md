---
title: Append 方法（ADOX 用户） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Users::raw_Append
- Users::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: b80bc5d5-78ca-4f75-956b-2ac658029cc7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 99a21cd5dd32af9e84877865cfe7c0fc92f6c087
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967226"
---
# <a name="append-method-adox-users"></a>Append 方法（ADOX 用户）
向[用户](../../../ado/reference/adox-api/users-collection-adox.md)集合添加新的[用户](../../../ado/reference/adox-api/user-object-adox.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>参数  
 *用户*  
 一个**变量**值，其中包含要追加的**用户**对象或要创建和追加的用户的名称。  
  
 *密码*  
 可选。 一个包含用户密码的**字符串**值。 *Password*参数与**User**对象的[ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md)方法所指定的值相对应。  
  
## <a name="remarks"></a>备注  
 [目录](../../../ado/reference/adox-api/catalog-object-adox.md)的**用户**集合表示所有目录的用户。 [组](../../../ado/reference/adox-api/group-object-adox.md)的**用户**集合仅表示在特定组中具有成员身份的用户。  
  
 如果提供程序不支持创建用户，则会发生错误。  
  
> [!NOTE]
>  将**用户**对象追加到**组**对象**的用户**集合之前，**目录**的**用户**集合中必须已经存在与要追加的用户[对象同名的](../../../ado/reference/adox-api/name-property-adox.md)**用户**对象。  
  
## <a name="applies-to"></a>应用于  
 [用户集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [组和用户追加，ChangePassword 方法示例（VB）](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 方法（ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法（ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法（ADOX 键）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法（ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法（ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
