---
title: Execute 方法 （ADO 命令） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4ef42c04944f39e0b2d1930cc6520df2b6c5fa5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918851"
---
# <a name="execute-method-ado-command"></a>Execute 方法（ADO 命令）
执行查询、 SQL 语句或存储的过程中指定[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)属性[命令对象](../../../ado/reference/ado-api/command-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>返回值  
 返回[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象的引用、 流或**Nothing**。  
  
#### <a name="parameters"></a>Parameters  
 *RecordsAffected*  
 可选。 一个**长**变量向其提供程序返回的操作所影响的记录数。 *RecordsAffected*参数仅适用于操作的查询或存储的过程。 *RecordsAffected*不返回的返回结果的查询或存储的过程返回的记录数。 若要获取此信息，请使用[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)属性。 **Execute**方法不会返回正确的信息与一起使用时**adAsyncExecute**，只需时以异步方式执行命令，因为受影响的记录数可能还不会知道在该方法返回的时间。  
  
 *Parameters*  
 可选。 一个**Variant**结合使用的输入的字符串或流中指定的参数值的数组**CommandText**或**CommandStream**。 （输出参数不会返回此参数中传递时的正确值。）  
  
 *选项*  
 可选。 一个**长**值，该值指示提供程序应该如何评估[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)属性的[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。 可以为使用所做的位掩码值[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)和/或[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值。 例如，可以使用**adCmdText**并**adExecuteNoRecords**结合，如果你想要具有计算的值的 ADO **CommandText**以文本形式的属性和指示该命令应放弃并返回执行命令文本时可能会生成任何记录。  
  
> [!NOTE]
>  使用**ExecuteOptionEnum**值**adExecuteNoRecords**通过最大程度减少内部处理来提高性能。 如果**adExecuteStream**指定了选项**adAsyncFetch**并**adAsynchFetchNonBlocking**将被忽略。 不要使用**CommandTypeEnum**的值**adCmdFile**或**adCmdTableDirect**与**Execute**。 这些值仅用作选项与[开放](../../../ado/reference/ado-api/open-method-ado-recordset.md)并[再次查询](../../../ado/reference/ado-api/requery-method.md)方法**记录集**。  
  
## <a name="remarks"></a>备注  
 使用**Execute**方法**命令**对象执行查询中指定**CommandText**属性或**CommandStream**对象的属性。  
  
 在返回结果**记录集**（默认） 或二进制信息的流。 若要获取的二进制流，请指定**adExecuteStream**中*选项*，然后通过设置提供的流**Command.Properties ("输出 Stream")** 。 ADO **Stream**可以指定对象以接收结果，或者可以指定另一个流对象，例如 IIS 响应对象。 如果没有流已指定，然后再调**Execute**与**adExecuteStream**，出现错误。 在从返回流的当前位置**Execute**是特定提供程序。  
  
 如果该命令不返回结果 （例如，SQL 更新查询） 访问接口将返回**Nothing**只要选项**adExecuteNoRecords**指定; 否则执行返回关闭**记录集**。 某些应用程序语言，可忽略此返回值，如果没有**记录集**所需的。  
  
 **执行**如果用户指定的值将引发错误**CommandStream**时**CommandType**是**adCmdStoredProc**， **adCmdTable**，或**adCmdTableDirect**。  
  
 如果查询具有参数，当前值为**命令**除非重写它们使用传递的参数值与使用对象的参数**Execute**调用。 您可以通过调用时省略的某些参数的新值替代参数的子集**Execute**方法。 在其中指定的参数的顺序是相同的顺序与方法传递它们。 例如，如果四个 （或多个） 参数，并且你想要传递的只有第一个和第四个参数的新值，将通过`Array(var1,,,var4)`作为*参数*参数。  
  
> [!NOTE]
>  输出参数不会返回正确的值时传入*参数*参数。  
  
 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)此操作结束时，将发出事件。  
  
> [!NOTE]
>  在发出包含 Url 的命令，使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [执行、 再次查询和清除方法示例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [执行、 再次查询和清除方法示例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [执行、 再次查询和清除方法示例 （VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandStream 属性 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [CommandText 属性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Execute 方法 （ADO 连接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [ExecuteComplete 事件 (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)
