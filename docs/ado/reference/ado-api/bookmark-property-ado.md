---
title: 书签属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bb835a84d83730e291afcfdf83910f9b520daea6
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696300"
---
# <a name="bookmark-property-ado"></a>Bookmark 属性 (ADO)
指示一个书签，用于唯一标识中的当前记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象或设置当前记录中**记录集**标识的有效书签记录的对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**变体**表达式的计算结果为有效的书签。  
  
## <a name="remarks"></a>备注  
 使用**书签**属性以保存当前记录的位置并在任何时候返回到该记录。 仅在中可用，书签将变为**记录集**支持书签功能的对象。  
  
 当打开**记录集**对象时，每个其记录具有一个唯一的书签。 若要保存当前记录的书签，请分配的值**书签**给一个变量的属性。 若要快速返回到该记录移到另一个记录之后，任何时候，设置**记录集**对象的**书签**属性设置为该变量的值。  
  
 用户可能不能以查看该书签的值。 此外，用户不应期望书签是直接比较，因为两个引用同一条记录的书签可能具有不同的值。  
  
 如果您使用[克隆](../../../ado/reference/ado-api/clone-method-ado.md)方法来创建一份**记录集**对象，**书签**原始和重复的属性设置**记录集**对象相同，并且可以互换使用。 但是，不能使用来自不同的书签**记录集**对象互换，即使它们创建从同一个源或命令。  
  
> [!NOTE]
>  **远程数据服务使用情况**客户端上使用时**记录集**对象，**书签**属性始终为可用。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [BOF、 EOF 和 Bookmark 属性示例 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、 EOF 和 Bookmark 属性示例 （VC + +）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
