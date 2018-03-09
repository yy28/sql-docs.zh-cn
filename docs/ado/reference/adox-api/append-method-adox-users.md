---
title: "Append 方法 （ADOX 用户） |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Users::raw_Append
- Users::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: b80bc5d5-78ca-4f75-956b-2ac658029cc7
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00652a3051d817c779fd45f546228163c72656fd
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="append-method-adox-users"></a>Append 方法 （ADOX 用户）
添加新[用户](../../../ado/reference/adox-api/user-object-adox.md)对象传递给[用户](../../../ado/reference/adox-api/users-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>Parameters  
 *用户*  
 A **Variant**值，该值包含**用户**要追加的对象或要创建并追加的用户的名称。  
  
 *密码*  
 選擇性。 A**字符串**值，该值包含用户的密码。 *密码*参数对应于指定的值[ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md)方法**用户**对象。  
  
## <a name="remarks"></a>注释  
 **用户**集合[目录](../../../ado/reference/adox-api/catalog-object-adox.md)表示目录的所有用户。 **用户**集合[组](../../../ado/reference/adox-api/group-object-adox.md)表示仅限拥有特定的组成员身份的用户。  
  
 如果提供程序不支持创建用户，将会出错。  
  
> [!NOTE]
>  在追加之前**用户**对象传递给**用户**集合**组**对象，**用户**对象具有相同[名称](../../../ado/reference/adox-api/name-property-adox.md)如要追加的一个必须已存在于**用户**集合**目录**。  
  
## <a name="applies-to"></a>适用范围  
 [用户集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [组和用户追加，ChangePassword 方法示例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 方法 （ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 键）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
