---
title: ParentCatalog 属性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User::get_ParentCatalog
- _Column::ParentCatalog
- _Table::put_ParentCatalog
- _Group::put_ParentCatalog
- _Column::get_ParentCatalog
- _Table::PutParentCatalog
- _Group::putref_ParentCatalog
- _Group::ParentCatalog
- _Column::PutParentCatalog
- _Column::put_ParentCatalog
- _Group::get_ParentCatalog
- _User::put_ParentCatalog
- _User::putref_ParentCatalog
- _Table::get_ParentCatalog
- _Group::PutParentCatalog
- _Table::ParentCatalog
- _Column::GetParentCatalog
- _Table::PutRefParentCatalog
- _User::GetParentCatalog
- _Table::GetParentCatalog
- _Table::putref_ParentCatalog
- _User::PutParentCatalog
- _User::ParentCatalog
- _User::PutRefParentCatalog
- _Group::GetParentCatalog
- _Group::PutRefParentCatalog
helpviewer_keywords:
- ParentCatalog property [ADOX]
ms.assetid: a0bb2ed8-d4cb-4f92-8de7-769bbe0e6273
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8bc9527109aaa4a3a8063b26a594c9bdb978dcf3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965582"
---
# <a name="parentcatalog-property-adox"></a>ParentCatalog 属性 (ADOX)
指定要提供对特定于提供程序的属性的访问的表、 用户或列对象的父目录。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置并返回[目录](../../../ado/reference/adox-api/catalog-object-adox.md)对象。 设置**ParentCatalog**向打开**目录**允许访问特定于提供程序的属性之前追加的表或列**目录**集合。  
  
## <a name="remarks"></a>备注  
 某些数据访问接口允许提供程序特定属性值仅在创建时写入： 即，当表或列追加到其**目录**集合。 若要访问这些属性，然后追加到这些对象再**目录**，指定**目录**中**ParentCatalog**属性第一个。  
  
 为另一种追加的表或列时出错**目录**比**ParentCatalog**。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[列对象 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|  
|[用户对象 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)||  
  
## <a name="see-also"></a>请参阅  
 [ParentCatalog 属性示例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
