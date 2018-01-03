---
title: "书签属性 (ADO) |Microsoft 文档"
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
f1_keywords: Recordset15::Bookmark
helpviewer_keywords: Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 498f1db6216d949663dba9bd22e8066534241605
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="bookmark-property-ado"></a>书签属性 (ADO)
指示一个书签，用于唯一标识中的当前记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象或设置当前记录中**记录集**到由有效的书签记录的对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**Variant**计算结果为有效的书签的表达式。  
  
## <a name="remarks"></a>Remarks  
 使用**书签**属性以保存当前记录的位置，并随时返回到该记录。 仅在中可用，书签将变为**记录集**支持书签功能的对象。  
  
 当你打开**记录集**对象时，每个其记录具有一个唯一的书签。 若要保存当前记录的书签，请将值指定**书签**给一个变量的属性。 若要快速返回到该记录移到另一条记录之后，任何时候，设置**记录集**对象的**书签**属性设置为该变量的值。  
  
 用户可能无法以查看该书签的值。 另外，用户不应期望书签以直接比较??? 两个引用同一个记录的书签可能具有不同的值。  
  
 如果你使用[克隆](../../../ado/reference/ado-api/clone-method-ado.md)方法来创建一份**记录集**对象，**书签**原始和重复的属性设置**记录集**对象是相同的而且你可以交替使用它们。 但是，不能使用通过不同的书签**记录集**对象互换，即使它们已创建从相同的源或命令。  
  
> [!NOTE]
>  **远程数据服务使用情况**时在客户端上使用**记录集**对象，**书签**属性是始终可用。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [BOF、 EOF，以及书签属性示例 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、 EOF 和书签属性示例 （VC + +）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
