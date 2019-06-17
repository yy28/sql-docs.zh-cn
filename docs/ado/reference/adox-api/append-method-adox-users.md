---
title: Append 方法 （ADOX 用户） |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 4c1f772b041aa5f7be2c1fc0c7aeb7c69189b5d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708341"
---
# <a name="append-method-adox-users"></a>Append 方法（ADOX 用户）
添加一个新[用户](../../../ado/reference/adox-api/user-object-adox.md)对象传递给[用户](../../../ado/reference/adox-api/users-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>Parameters  
 *用户*  
 一个**Variant**值，该值包含**用户**对象以追加或要创建并追加的用户的名称。  
  
 *密码*  
 可选。 一个**字符串**值，该值包含用户的密码。 *密码*参数对应于指定的值[ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md)方法**用户**对象。  
  
## <a name="remarks"></a>备注  
 **用户**系列[目录](../../../ado/reference/adox-api/catalog-object-adox.md)表示目录的所有用户。 **用户**集合[组](../../../ado/reference/adox-api/group-object-adox.md)表示仅拥有特定的组成员身份的用户。  
  
 如果提供程序不支持创建用户，将会出错。  
  
> [!NOTE]
>  之前追加**用户**对象传递给**用户**的集合**组**对象，**用户**对象具有相同[名称](../../../ado/reference/adox-api/name-property-adox.md)如要追加的一个必须已存在于**用户**的集合**目录**。  
  
## <a name="applies-to"></a>适用范围  
 [用户集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>请参阅  
 [组和用户 Append、 ChangePassword 方法示例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 方法 （ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 项）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
