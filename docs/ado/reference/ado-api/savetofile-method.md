---
title: SaveToFile 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1b3a94fddf1ac439096e2e0106fb2becb79249c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711334"
---
# <a name="savetofile-method"></a>SaveToFile 方法
将保存的二进制内容组成[Stream](../../../ado/reference/ado-api/stream-object-ado.md)到文件。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>Parameters  
 *FileName*  
 一个**字符串**值，该值包含到的文件的完全限定名称的内容**Stream**将保存。 您可以将其保存到任何有效的本地位置，或你有权访问通过 UNC 值的任何位置。  
  
 *SaveOptions*  
 一个[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)值，该值指定是否应通过创建一个新的文件**SaveToFile**，如果尚不存在。 默认值是**adSaveCreateNotExists**。 通过这些选项可以指定是否指定的文件不存在，就会出错。 您还可以指定**SaveToFile**将覆盖现有文件的当前内容。  
  
> [!NOTE]
>  如果覆盖现有文件 (当**adSaveCreateOverwrite**设置)， **SaveToFile**将遵循新的任何字节的原始的现有文件的截断[EOS](../../../ado/reference/ado-api/eos-property.md)。  
  
## <a name="remarks"></a>备注  
 **SaveToFile**可用于复制的内容**Stream**到本地文件的对象。 中的内容或属性的没有变化**Stream**对象。 **Stream**对象必须在打开之前调用**SaveToFile**。  
  
 此方法不会更改的关联**Stream**到其基础源对象。 **Stream**对象将仍与相关联的原始 URL 或**记录**已打开时其源。  
  
 之后**SaveToFile**操作，当前的位置 ([位置](../../../ado/reference/ado-api/position-property-ado.md)) 流中设置为流 (0) 的开始位置。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
