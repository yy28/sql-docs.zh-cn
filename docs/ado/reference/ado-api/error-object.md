---
title: 错误对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5018dc921267663d64037024ef21c82ac6e3f7c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932960"
---
# <a name="error-object"></a>错误对象
包含有关适用于单个操作涉及该提供程序的数据访问错误的详细信息。  
  
## <a name="remarks"></a>备注  
 任何涉及 ADO 对象的操作可以生成一个或多个提供程序错误。 每个错误发生时，一个或多个**错误**对象都将置于[错误](../../../ado/reference/ado-api/errors-collection-ado.md)的集合[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。 当另一个 ADO 操作生成一个错误，**错误**清除集合，和一组新的**错误**对象置于**错误**集合。  
  
> [!NOTE]
>  每个**错误**对象都表示特定的提供程序错误，而不是 ADO 错误。 ADO 错误公开给运行时异常处理机制。 例如，在 Microsoft Visual Basic 中，特定于 ADO 的错误的匹配项将触发**On Error**事件并显示在**错误**对象。 ADO 错误的完整列表，请参阅[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)主题。  
  
 可以读取**错误**对象的属性来获取有关每个错误，包括以下特定详细信息：  
  
-   [说明](../../../ado/reference/ado-api/description-property.md)属性，其中包含错误的文本。 这是默认属性。  
  
-   [数量](../../../ado/reference/ado-api/number-property-ado.md)属性，其中包含**长**错误常量的整数值。  
  
-   [源](../../../ado/reference/ado-api/source-property-ado-error.md)属性，用于标识引发了错误的对象。 这是特别有用的当有多个**错误**中的对象**错误**遵循一个请求到数据源的集合。  
  
-   [SQLState](../../../ado/reference/ado-api/sqlstate-property.md)并[NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)属性，它们提供从 SQL 数据源的信息。  
  
 提供程序错误时，将其放**错误**系列**连接**对象。 ADO 支持通过单个 ADO 操作以允许错误的信息特定于提供程序返回多个错误。 若要获取此丰富的错误消息的错误处理程序中，使用相应的错误捕获功能的语言或环境正在使用，然后使用嵌套的循环来枚举每个属性**错误**对象中**错误**集合。  
  
> [!NOTE]
>  **Microsoft Visual Basic 和 VBScript 用户**如果没有有效**连接**对象，您需要错误从中检索信息**错误**对象。  
  
 正如提供程序执行操作，ADO 清除**OLE 错误信息**对象，然后才能进行调用，可能无法生成新的提供程序错误。 但是，**错误**上的收集**连接**对象被清除并且仅当提供程序生成一个新的错误，或填充[清除](../../../ado/reference/ado-api/clear-method-ado.md)调用方法。  
  
 某些属性和方法返回显示为警告**错误**中的对象**错误**集合但不是会停止程序执行。 在调用之前[重新同步](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)上的方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象;[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法**连接**对象; 或者设置[筛选器](../../../ado/reference/ado-api/filter-property.md)属性**记录集**对象，请调用**清除**上的方法**错误**集合。 这样一来，可以读取[计数](../../../ado/reference/ado-api/count-property-ado.md)的属性**错误**集合以测试是否返回警告。  
  
 **错误**对象不是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [错误对象属性、方法和事件](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、 HelpContext、 HelpFile、 NativeError、 数、 源和 SQLState 属性示例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [错误集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
