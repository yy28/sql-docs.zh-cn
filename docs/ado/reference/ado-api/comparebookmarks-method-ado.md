---
title: CompareBookmarks 方法 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85ca76678c0d3e75a106164626c4e3c3a81bd7e9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649745"
---
# <a name="comparebookmarks-method-ado"></a>CompareBookmarks 方法 (ADO)
比较两个书签，并返回其相对值的指示。  
  
## <a name="syntax"></a>语法  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>返回值  
 返回[CompareEnum](../../../ado/reference/ado-api/compareenum.md)值，该值指示由其书签的两条记录的相对行位置。  
  
#### <a name="parameters"></a>Parameters  
 *Bookmark1*  
 第一行的书签。  
  
 *Bookmark2*  
 第二行的书签。  
  
## <a name="remarks"></a>备注  
 书签必须应用到同一[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，或**记录集**对象并将其[克隆](../../../ado/reference/ado-api/clone-method-ado.md)。 您不能可靠地比较来自不同的书签**记录集**对象，即使它们创建从同一个源或命令。 也可以进行比较的书签**记录集**其基础提供程序不支持比较的对象。  
  
 一个书签，唯一标识中的某一行**记录集**对象。 使用[书签](../../../ado/reference/ado-api/bookmark-property-ado.md)要获取其书签的当前行的属性。  
  
 一个书签的数据类型是特定于每个提供程序，因为 ADO 公开其作为**变体**。 例如，SQL Server，书签将变为类型 DBTYPE_R8 的 (**Double**)。 ADO 将公开此类型作为**Variant**使用的子类型**Double**。  
  
 在比较书签时，ADO 将不会尝试任何类型的强制转换。 将值只被传递给提供程序进行比较。 如果传递给书签**CompareBookmarks**方法存储在不同类型的变量，它可以生成以下类型不匹配错误:"自变量的类型不正确、 不在可接受范围内，或发生冲突与每个其他。  
  
 一个书签，用于无效或格式不正确会导致错误。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [CompareBookmarks 方法示例 (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [CompareBookmarks 方法示例 （VC + +）](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Bookmark 属性 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
