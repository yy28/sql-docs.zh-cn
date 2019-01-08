---
title: Open 方法 （ADO 记录集） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Open
- Recordset15::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 3236749c-4b71-4235-89e2-ccdfaaa9319d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2b02ac3d8e95bb583515dfa780f473402ea798f
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206316"
---
# <a name="open-method-ado-recordset"></a>Open 方法（ADO 记录集）
在打开一个游标[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>Parameters  
 *数据源*  
 可选。 一个**Variant**的计算结果为有效[命令](../../../ado/reference/ado-api/command-object-ado.md)对象、 SQL 语句、 表名、 存储的过程调用、 一个 URL 或文件的名称或[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象，其中包含持久地存储[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 *ActiveConnection*  
 可选。 任一**Variant**的计算结果为有效[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象变量名称，或**字符串**，其中包含[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)参数。  
  
 *CursorType*  
 可选。 一个[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)值，该值确定的提供程序应使用时打开的游标类型**记录集**。 默认值是**adOpenForwardOnly**。  
  
 *LockType*  
 可选。 一个[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值，该值确定哪种类型的锁定 （并发） 提供程序应使用打开时**记录集**。 默认值是**adLockReadOnly**。  
  
 *选项*  
 可选。 一个**长**值，该值指示提供程序应该如何评估*源*参数，如果它不是表示内容**命令**对象，或者**记录集**应该从以前已保存的文件进行还原。 可以是一个或多个[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)或[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)可以使用按位 OR 运算符组合的值。  
  
> [!NOTE]
>  如果您打开**记录集**从**Stream**包含的持久化**记录集**，并使用[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 值**adAsyncFetchNonBlocking**不会产生影响; 提取将同步和正在阻塞。  
  
> [!NOTE]
>  **ExecuteOpenEnum**的值**adExecuteNoRecords**或**adExecuteStream**不能与**打开**。  
  
## <a name="remarks"></a>备注  
 ADO 的默认光标**记录集**是位于服务器上的只进、 只读游标。  
  
 使用**开放**方法**记录集**对象打开一个游标，从基础表、 一个查询，或以前保存的结果表示记录**记录集**。  
  
 使用可选*源*参数，以指定数据源使用以下值之一：**命令**对象变量、 SQL 语句、 存储的过程、 表名称、 一个 URL 或完整文件路径名称。 如果*源*是文件路径名称，它可以是完整路径 ("c:\dir\file.rst") 的相对路径 ("...\file.rst")，或 URL ("<https://files/file.rst>")。  
  
 它不是使用一个好办法*源*的参数**打开**方法以执行动作查询不返回记录，因为没有简单方法来确定调用是否成功。 **记录集**返回的此类查询将被关闭。 若要执行的查询不返回记录，如 SQL INSERT 语句中，调用[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法**命令**对象或[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
 *ActiveConnection*参数对应于[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性，并指定要打开的连接中**记录集**对象。 如果通过连接定义为此参数，ADO 将打开一个新的连接，使用指定的参数。 打开后**记录集**与通过设置客户端游标[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**，可以更改将发送此属性的值对另一个提供程序的更新。 也可以设置此属性为**Nothing** (Microsoft Visual Basic 中) 或为 NULL，以断开连接**记录集**从任何提供程序。 更改*ActiveConnection*为服务器端游标生成一个错误，但是。  
  
 直接对应的属性的其他自变量**记录集**对象 (*源*， *CursorType*，以及*LockType*)，属性的自变量的关系如下所示：  
  
-   该属性为读/写之前**记录集**打开对象。  
  
-   如果在执行时传递相应的参数，则使用的属性设置**打开**方法。 如果传递参数，它将替代相应的属性设置，并使用参数值更新该属性设置。  
  
-   打开后**记录集**对象，这些属性将变为只读的。  
  
> [!NOTE]
>  **ActiveConnection**属性是只读的**记录集**对象其[源](../../../ado/reference/ado-api/source-property-ado-recordset.md)属性设置为有效**命令**对象，即使**记录集**对象未打开。  
  
 如果传递**命令**对象中*源*自变量以及传递*ActiveConnection*参数，就会出错。 **ActiveConnection**的属性**命令**对象必须已设置为有效**连接**对象或连接字符串。  
  
 如果传递的内容以外**命令**对象中*源*参数，可以使用*选项*参数来优化评估*源*参数。 如果*选项*未定义参数，因为 ADO 必须进行到提供程序的调用，以确定参数是否为 SQL 语句、 存储的过程、 一个 URL 或表名，可能会遇到性能降低的程度。 如果您知道什么*源*类型使用的，设置*选项*参数指示 ADO 直接跳转到相关代码。 如果*选项*参数不匹配*源*键入时，出现错误。  
  
 如果传递**Stream**对象中*源*参数，您应不将信息传递到其他参数。 执行此操作将生成错误。 **ActiveConnection**信息不是保留时**记录集**从打开**Stream**。  
  
 默认值为*选项*自变量是**adCmdFile**如果没有连接与相关联**记录集**。 这对于持久地存储通常是这种情况**记录集**对象。  
  
 如果数据源未不返回任何记录，该提供程序设置[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)和[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性设置为**True**，并将当前记录的位置是不确定。 仍可以将新数据添加到此空**记录集**对象的游标类型允许它。  
  
 当通过一个打开结束您的运营**记录集**对象，请使用[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法来释放任何关联的系统资源。 关闭对象不会删除它从内存;可以更改其属性设置，并使用**打开**方法稍后再打开它。 若要完全消除从内存对象，请将对象变量设置为*Nothing*。  
  
 之前**ActiveConnection**属性设置，则调用**打开**使用创建的实例没有操作数**记录集**通过追加到的字段创建**记录集**[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合。  
  
 如果设置了[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**，可以检索以异步方式在两种方式之一中的行。 建议的方法是设置*选项*到**adAsyncFetch**。 或者，可以使用中的"异步行集处理"的动态属性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，但检索到的相关的事件可能会丢失如果未设置*选项*参数**adAsyncFetch**。  
  
> [!NOTE]
>  背景提取 MS 远程提供程序中只能通过支持**开放**方法的*选项*参数。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 某些组合[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)并[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值均无效。 有关哪些选项不能结合使用的信息，请参阅主题[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)，并[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Open 和 Close 方法示例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 和 Close 方法示例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 和 Close 方法示例 （VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Save 和 Open 方法示例 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Open 方法 （ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
