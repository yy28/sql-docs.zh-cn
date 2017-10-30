---
title: "执行方法 （ADO 命令） |Microsoft 文档"
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
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 651123d3112ca58c028412bd025325f303f0d637
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-ado-command"></a>执行方法 （ADO 命令）
执行查询、 SQL 语句或存储的过程中指定[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)属性[命令对象](../../../ado/reference/ado-api/command-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>返回值  
 返回[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象引用、 流、 或**执行任何操作**。  
  
#### <a name="parameters"></a>Parameters  
 *RecordsAffected*  
 可选。 A**长**变量到该提供程序返回的操作所影响的记录数。 *RecordsAffected*参数仅适用于操作查询或存储的过程。 *RecordsAffected*不返回的返回结果的查询或存储的过程返回的记录数。 若要获取此信息，请使用[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)属性。 **执行**方法不会返回正确的信息一起使用时**adAsyncExecute**，只需时以异步方式执行命令，因为受影响的记录数可能尚未未知在该方法返回的时间。  
  
 *参数*  
 可选。 A **Variant**与输入的字符串或流中指定结合使用的参数值数组**CommandText**或**CommandStream**。 （输出参数不会返回此参数中传递时的正确值。）  
  
 *选项*  
 可选。 A**长**值，该值指示提供程序应如何评估[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)属性[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。 可以是使用所做的位掩码值[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)和/或[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值。 例如，可以使用**adCmdText**和**adExecuteNoRecords**结合，如果你想要评估的值的 ADO **CommandText**属性作为文本，并指示该命令应放弃，并且不会返回命令文本执行时可能会生成任何记录。  
  
> [!NOTE]
>  使用**ExecuteOptionEnum**值**adExecuteNoRecords**通过最小化内部处理来提高性能。 如果**adExecuteStream**已指定，选项**adAsyncFetch**和**adAsynchFetchNonBlocking**将被忽略。 不要使用**CommandTypeEnum**值**adCmdFile**或**adCmdTableDirect**与**执行**。 这些值仅用作选项[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)和[Requery](../../../ado/reference/ado-api/requery-method.md)方法**记录集**。  
  
## <a name="remarks"></a>注释  
 使用**执行**方法**命令**对象执行中指定的查询**CommandText**属性或**CommandStream**对象的属性。  
  
 返回结果的顺序**记录集**（默认） 或作为二进制信息的流。 若要获取二进制流，请指定**adExecuteStream**中*选项*，则通过设置提供流**Command.Properties （"输出流"）**。 ADO**流**可以指定对象接收结果，或可以指定另一个流对象，如 IIS 响应对象。 如果没有流已指定，然后再调**执行**与**adExecuteStream**，发生错误。 从返回流的当前位置**执行**是特定提供程序。  
  
 如果该命令不是要返回的结果 （例如，SQL 更新查询） 该提供程序返回**执行任何操作**只要选项**adExecuteNoRecords**指定; 否则将执行返回关闭**记录集**。 某些应用程序语言，可以忽略此返回值，如果没有**记录集**需要。  
  
 **执行**引发错误，如果用户指定的值**CommandStream**时**CommandType**是**adCmdStoredProc**， **adCmdTable**，或**adCmdTableDirect**。  
  
 如果查询具有参数，当前值为**命令**除非重写这些与传递的参数值使用对象的参数**执行**调用。 你可以通过调用时省略的某些参数的新值替代的参数的子集**执行**方法。 指定参数的顺序是相同的顺序与方法传递它们。 例如，如果没有四个 （或多个） 参数，并且你想要将新值仅的第一个和第四个参数传递，将通过`Array(var1,,,var4)`作为*参数*自变量。  
  
> [!NOTE]
>  输出参数不会返回正确的值，当传入*参数*自变量。  
  
 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)此操作结束时，将发出事件。  
  
> [!NOTE]
>  当发出命令包含的 Url，那些使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [执行、 重新执行查询，并清除方法示例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [执行、 重新执行查询，并清除方法示例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [执行、 重新执行查询，并清除方法示例 （VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandStream 属性 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [CommandText 属性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [执行方法 （ADO 连接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [ExecuteComplete 事件 (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)

