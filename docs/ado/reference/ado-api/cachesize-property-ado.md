---
title: "CacheSize 属性 (ADO) |Microsoft 文档"
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
f1_keywords: Recordset15::CacheSize
helpviewer_keywords: CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a035843f42ba6dd29f18887fec5ca334943a0df4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="cachesize-property-ado"></a>CacheSize 属性 (ADO)
指示返回的记录数[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)本地缓存在内存中的对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**必须大于 0 的值。 默认值为 1。  
  
## <a name="remarks"></a>Remarks  
 使用**CacheSize**属性控制将在一次检索到从提供程序的本地内存的记录数。 例如，如果**CacheSize**后第一个左为 10，**记录集**对象，该提供程序检索前 10 条记录到本地内存。 当你移动通过**记录集**对象，该提供程序从本地内存缓冲区中返回数据。 一旦移过缓存中的最后一个记录，即会将提供程序会将从数据源的接下来的 10 的记录检索到缓存中。  
  
> [!NOTE]
>  **CacheSize**基于**打开的最大行数**提供程序特定属性 (在**属性**集合**记录集**对象)。 无法设置**CacheSize**为值大于**打开的最大行数**。 若要修改的提供程序可以打开的行数，设置**打开的最大行数**。  
  
 值**CacheSize**进行调整的生命周期内**记录集**对象，但更改此值仅影响在缓存中的记录数后的后续检索的数据源。 更改属性值本身不会更改当前缓存的内容。  
  
 如果没有较少的记录，可供检索比**CacheSize**指定，该提供程序返回剩下的记录，且不发生错误。  
  
 A **CacheSize**设置为零时不允许，并返回错误。  
  
 从缓存中检索的记录不能反映其他用户对源数据所做的并发更改。 若要强制执行更新的所有缓存的数据，使用[重新同步](../../../ado/reference/ado-api/resync-method.md)方法。  
  
 如果**CacheSize**设置为值大于 1 的浏览方法 ([移动](../../../ado/reference/ado-api/move-method-ado.md)， [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) 可能会导致导航到删除记录，如果删除发生后已检索的记录。 后初始提取，后续的删除将不会反映在你的数据缓存之前尝试访问从已删除的行的数据值。 但是，将设置**CacheSize**到其中一个消除此问题无法提取已删除的行之后。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [CacheSize 属性示例 (VB)](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [CacheSize 属性示例 （VC + +）](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [CacheSize 属性示例 (JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)
