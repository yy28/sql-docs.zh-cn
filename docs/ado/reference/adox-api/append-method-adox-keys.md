---
title: Append 方法 （ADOX 项） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Keys::Append
- Keys::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 215a5391-f422-42ec-99ea-4e6fbb5d3d64
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd66edb75bec4f4b7e35c53c9ebeabd9b3c75d83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967299"
---
# <a name="append-method-adox-keys"></a>Append 方法（ADOX 项）
添加一个新[键](../../../ado/reference/adox-api/key-object-adox.md)对象传递给[密钥](../../../ado/reference/adox-api/keys-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>Parameters  
 *Key*  
 **密钥**对象以追加或创建并追加的密钥的名称。  
  
 *KeyType*  
 可选。 一个**长**值，该值指定键的类型。 *键*参数对应于[类型](../../../ado/reference/adox-api/type-property-key-adox.md)属性**密钥**对象。  
  
 *列*  
 可选。 一个**字符串**值，该值指定要编制索引的列的名称。 *列*参数对应的值[名称](../../../ado/reference/adox-api/name-property-adox.md)属性[列](../../../ado/reference/adox-api/column-object-adox.md)对象。  
  
 *RelatedTable*  
 可选。 一个**字符串**值，该值指定在相关表的名称。 *RelatedTable*参数对应的值**名称**属性[表](../../../ado/reference/adox-api/table-object-adox.md)对象。  
  
 *RelatedColumn*  
 可选。 一个**字符串**值，该值指定外键的相关列的名称。 *RelatedColumn*参数对应的值**名称**属性[列](../../../ado/reference/adox-api/column-object-adox.md)对象。  
  
## <a name="remarks"></a>备注  
 *列*参数可以采用的一列的名称或列名称的数组。  
  
## <a name="applies-to"></a>适用范围  
 [项集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>请参阅  
 [项 Append 方法、 密钥类型、 RelatedColumn、 RelatedTable 和 UpdateRule 属性示例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Append 方法 （ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 （ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
