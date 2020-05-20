---
title: CompareBookmarks 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords:
- CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
author: rothja
ms.author: jroth
ms.openlocfilehash: aa4be74086e4d35af70ac52aa9db0066f4279e3e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760363"
---
# <a name="comparebookmarks-method-ado"></a>CompareBookmarks 方法 (ADO)
比较两个书签，并返回其相对值的指示值。  
  
## <a name="syntax"></a>语法  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>返回值  
 返回一个[CompareEnum](../../../ado/reference/ado-api/compareenum.md)值，该值指示由其书签表示的两个记录的相对行位置。  
  
#### <a name="parameters"></a>参数  
 *Bookmark1*  
 第一行的书签。  
  
 *Bookmark2*  
 第二行的书签。  
  
## <a name="remarks"></a>备注  
 书签必须应用于相同的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象或**记录集**对象及其[克隆](../../../ado/reference/ado-api/clone-method-ado.md)。 不能从不同的**记录集**对象中可靠地比较书签，即使它们是从同一源或命令创建的也是如此。 您也不能对其基础提供程序不支持比较的**记录集**对象的书签进行比较。  
  
 书签唯一标识**Recordset**对象中的行。 使用当前行的 "[书签](../../../ado/reference/ado-api/bookmark-property-ado.md)" 属性获取其书签。  
  
 由于书签的数据类型特定于每个提供程序，因此 ADO 将其作为**变量**公开。 例如，SQL Server 书签的类型为 DBTYPE_R8 （**Double**）。 ADO 将此类型公开为具有**双精度**类型的**变体**。  
  
 比较书签时，ADO 不尝试任何类型的强制。 这些值只传递到进行比较的访问接口。 如果传递给**CompareBookmarks**方法的书签存储在不同类型的变量中，则它可能会生成以下类型不匹配错误： "参数的类型错误，超出了可接受的范围，或相互冲突。"  
  
 无效或格式不正确的书签将导致错误。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [CompareBookmarks 方法示例（VB）](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [CompareBookmarks 方法示例（VC + +）](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Bookmark 属性 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
