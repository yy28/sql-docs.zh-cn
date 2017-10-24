---
title: "错误对象 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a283d7d40140e46668dc704196316a4a52c1fdbf
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="error-object"></a>错误对象
包含有关适用于涉及提供程序的单个操作的数据访问错误的详细信息。  
  
## <a name="remarks"></a>注释  
 涉及 ADO 对象的任何操作可以生成一个或多个提供程序错误。 每个错误发生时，一个或多个**错误**对象都将置于[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。 当另一个 ADO 操作生成错误，**错误**集合处于未选中状态，以及新的集**错误**对象放入**错误**集合。  
  
> [!NOTE]
>  每个**错误**对象表示特定的提供程序错误，而不是 ADO 错误。 ADO 错误公开给运行时异常处理机制。 例如，在 Microsoft Visual Basic，ADO 特定错误的匹配项将触发**On Error**事件并显示在**错误**对象。 ADO 错误的完整列表，请参阅[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)主题。  
  
 你可以阅读**错误**对象的属性来获取有关每个错误，包括以下的特定详细信息：  
  
-   [说明](../../../ado/reference/ado-api/description-property.md)属性，其中包含错误的文本。 这是默认属性。  
  
-   [数](../../../ado/reference/ado-api/number-property-ado.md)属性，其中包含**长**错误常量的整数值。  
  
-   [源](../../../ado/reference/ado-api/source-property-ado-error.md)属性，它标识引发错误的对象。 当可以通过多种方式，这一点特别有用**错误**中的对象**错误**以下到数据源的请求的集合。  
  
-   [SQLState](../../../ado/reference/ado-api/sqlstate-property.md)和[NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)属性，它们提供来自 SQL 数据源的信息。  
  
 提供程序错误时，则将其放入**错误**集合**连接**对象。 ADO 支持通过单个 ADO 操作以允许错误信息特定于所提供的多个错误返回。 若要获取此丰富的错误信息，错误处理程序中，使用的语言或正在使用的环境的相应错误捕获功能，然后使用嵌套的循环来枚举每个属性**错误**对象中**错误**集合。  
  
> [!NOTE]
>  **Microsoft Visual Basic 和 VBScript 用户**如果没有有效**连接**对象，你将需要检索错误信息从**错误**对象。  
  
 为提供程序执行操作，ADO 清除**OLE 错误信息**对象，然后再进行调用，可能无法生成新的提供程序错误。 但是，**错误**集合**连接**对象被清除，并且仅当在提供程序生成一个新的错误，或填充[清除](../../../ado/reference/ado-api/clear-method-ado.md)调用方法。  
  
 某些属性和方法返回显示为警告**错误**中的对象**错误**集合但不是会停止对程序的执行。 在调用之前[重新同步](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象;[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法**连接**对象; 或设置[筛选器](../../../ado/reference/ado-api/filter-property.md)属性**记录集**对象，请调用**清除**方法**错误**集合。 这样一来，你可以阅读[计数](../../../ado/reference/ado-api/count-property-ado.md)属性**错误**集合以测试是否返回警告。  
  
 **错误**对象不是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [错误对象属性、 方法和事件](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [描述、 HelpContext、 HelpFile、 NativeError、 数量、 源和 SQLState 属性示例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 HelpFile、 NativeError、 数量、 源和 SQLState 属性示例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [错误集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [附录 a： 提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)

