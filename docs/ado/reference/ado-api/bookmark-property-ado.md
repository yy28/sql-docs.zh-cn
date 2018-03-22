---
title: 书签属性 (ADO) |Microsoft 文档
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 59cc184403fff8b152ee7eabbdf823abd6c3d4bc
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="bookmark-property-ado"></a>书签属性 (ADO)
指示一个书签，用于唯一标识中的当前记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象或设置当前记录中**记录集**到由有效的书签记录的对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**Variant**计算结果为有效的书签的表达式。  
  
## <a name="remarks"></a>注释  
 使用**书签**属性以保存当前记录的位置，并随时返回到该记录。 仅在中可用，书签将变为**记录集**支持书签功能的对象。  
  
 当你打开**记录集**对象时，每个其记录具有一个唯一的书签。 若要保存当前记录的书签，请将值指定**书签**给一个变量的属性。 若要快速返回到该记录移到另一条记录之后，任何时候，设置**记录集**对象的**书签**属性设置为该变量的值。  
  
 用户可能无法以查看该书签的值。 此外，用户不应期望书签直接比较，因为需要两个引用同一个记录的书签可能具有不同的值。  
  
 如果你使用[克隆](../../../ado/reference/ado-api/clone-method-ado.md)方法来创建一份**记录集**对象，**书签**原始和重复的属性设置**记录集**对象是相同的而且你可以交替使用它们。 但是，不能使用通过不同的书签**记录集**对象互换，即使它们已创建从相同的源或命令。  
  
> [!NOTE]
>  **远程数据服务使用情况**时在客户端上使用**记录集**对象，**书签**属性是始终可用。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [BOF、 EOF，以及书签属性示例 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、 EOF 和书签属性示例 （VC + +）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
