---
title: "SaveToFile 方法 |Microsoft 文档"
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
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords: SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5a515534601696c0ca056f573c179c5e00bac3e0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="savetofile-method"></a>SaveToFile 方法
将保存的二进制内容组成[流](../../../ado/reference/ado-api/stream-object-ado.md)到文件。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>Parameters  
 *FileName*  
 A**字符串**包含到的文件的完全限定名称的值的内容**流**将保存。 你可以将其保存到任何有效的本地位置，或可以访问通过 UNC 值的任何位置。  
  
 *SaveOptions*  
 A [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)值，该值指定是否应通过创建新文件**SaveToFile**，如果不存在。 默认值是**adSaveCreateNotExists**。 使用以下选项中，你可以指定是否指定的文件不存在，就会出错。 你还可以指定**SaveToFile**将覆盖现有文件的当前内容。  
  
> [!NOTE]
>  如果覆盖现有文件 (时**adSaveCreateOverwrite**设置)， **SaveToFile**截断按照新的原始的现有文件任何字节[EOS](../../../ado/reference/ado-api/eos-property.md)。  
  
## <a name="remarks"></a>Remarks  
 **SaveToFile**可能使用的内容复制**流**到本地文件的对象。 不没有中的内容或属性的任何更改**流**对象。 **流**对象必须是打开之前调用**SaveToFile**。  
  
 此方法不会更改的关联**流**与其基础数据源的对象。 **流**对象仍将与原始的 URL 关联或**记录**已打开时其源。  
  
 后**SaveToFile**当前位置、 操作 ([位置](../../../ado/reference/ado-api/position-property-ado.md)) 流中设置为流 (0) 的开始位置。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Open 方法 （ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
