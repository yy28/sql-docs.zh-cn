---
title: "Open 方法 （ADO 记录集） |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::raw_Open
- Recordset15::Open
helpviewer_keywords: Open method [ADO]
ms.assetid: 3236749c-4b71-4235-89e2-ccdfaaa9319d
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 3f223702a882910354d69fbcbfe5920e444000f7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="open-method-ado-recordset"></a>Open 方法 （ADO 记录集）
上打开一个游标[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>Parameters  
 *数据源*  
 可选。 A **Variant**计算结果为有效[命令](../../../ado/reference/ado-api/command-object-ado.md)对象、 SQL 语句、 表名、 存储的过程调用、 URL 或文件的名称或[流](../../../ado/reference/ado-api/stream-object-ado.md)对象，其中包含永久存储[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 *ActiveConnection*  
 可选。 任一**Variant**计算结果为有效[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象变量名称，或**字符串**包含[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)参数。  
  
 *游标类型*  
 可选。 A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)值，该值确定的提供程序打开时应使用的游标类型**记录集**。 默认值是**adOpenForwardOnly**。  
  
 *LockType*  
 可选。 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值，该值确定哪种类型的锁定 （并发） 提供程序应使用打开时**记录集**。 默认值是**adLockReadOnly**。  
  
 *选项*  
 可选。 A**长**值，该值指示提供程序应如何评估*源*参数如果以外表示的一些东西**命令**对象，或**记录集**应从以前已保存的文件还原。 可以是一个或多个[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)或[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)可以使用按位 OR 运算符组合的值。  
  
> [!NOTE]
>  如果你打开**记录集**从**流**包含持久化**记录集**，使用[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 值**adAsyncFetchNonBlocking**不会有影响; 提取将同步和阻塞。  
  
> [!NOTE]
>  **ExecuteOpenEnum**值**adExecuteNoRecords**或**adExecuteStream**不应与使用**打开**。  
  
## <a name="remarks"></a>注释  
 ADO 的默认光标**记录集**是位于服务器上的只进、 只读游标。  
  
 使用**打开**方法**记录集**对象打开的游标可用于表示从基础表、 查询或以前保存的结果的记录**记录集**。  
  
 使用可选*源*自变量以指定数据源使用以下项之一：**命令**对象变量、 SQL 语句、 存储的过程、 表名、 URL 或完整文件路径名称。 如果*源*是文件路径名称，它可以是的完整路径 ("c:\dir\file.rst") 的相对路径 ("...\file.rst")，或 URL ("http://files/file.rst")。  
  
 它不是使用一个好办法*源*参数**打开**方法来执行的操作查询，不返回记录，因为没有简单方法来确定调用是否成功。 **记录集**返回的此类查询将被关闭。 若要执行的查询不返回记录，例如 SQL INSERT 语句，调用[执行](../../../ado/reference/ado-api/execute-method-ado-command.md)方法**命令**对象或[执行](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
 *ActiveConnection*参数对应于[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性，并指定在哪种连接以打开**记录集**对象。 如果您传入的连接定义为此参数，ADO 将打开一个新的连接，使用指定的参数。 打开后**记录集**与客户端游标通过设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性**adUseClient**，你可以更改要发送此属性的值到其他提供商的更新。 你可以将此属性设置为或者**执行任何操作**(在 Microsoft Visual Basic) 或为 NULL 以断开连接**记录集**从任何提供程序。 更改*ActiveConnection*为服务器端游标会产生错误，但是。  
  
 直接对应的属性的其他自变量**记录集**对象 (*源*，*游标类型*，和*LockType*)，属性的自变量的关系如下所示：  
  
-   属性为读/写之前**记录集**打开对象。  
  
-   除非在执行时传递相应的参数，将使用的属性设置**打开**方法。 如果传递了参数，它将替代相应的属性设置，并使用自变量的值更新的属性设置。  
  
-   打开后**记录集**对象，这些属性将变为只读的。  
  
> [!NOTE]
>  **ActiveConnection**属性是只读的**记录集**对象其[源](../../../ado/reference/ado-api/source-property-ado-recordset.md)属性设置为有效**命令**对象，即使**记录集**对象未打开。  
  
 如果你通过**命令**对象在*源*自变量以及传递*ActiveConnection*自变量，就会出错。 **ActiveConnection**属性**命令**对象必须已设置为有效**连接**对象或连接字符串。  
  
 如果传递内容以外**命令**对象在*源*自变量，你可以使用*选项*参数来优化计算*源*自变量。 如果*选项*未定义参数，因为 ADO 必须进行到提供程序的调用，以确定参数是否为 SQL 语句、 存储的过程、 一个 URL 或表名，可能会遇到性能降低的程度。 如果你知道什么*源*正在使用，设置的类型*选项*参数指示 ADO 直接跳转到相关的代码。 如果*选项*自变量不匹配*源*类型，则会出错。  
  
 如果你通过**流**对象在*源*自变量，你应不将信息传递到其他自变量。 执行此操作将生成错误。 **ActiveConnection**信息不是保留时**记录集**从打开**流**。  
  
 默认值为*选项*自变量是**adCmdFile**如果没有连接与**记录集**。 这通常会是这种情况，永久存储**记录集**对象。  
  
 如果数据源未不返回任何记录，该提供程序设置同时[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)和[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性设置为**True**，而且当前的记录位置是不确定。 你仍然可以将新数据添加到此空**记录集**对象如果游标类型允许它。  
  
 当你结束您的操作通过一个打开**记录集**对象，请使用[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法释放任何关联系统资源。 关闭对象不会删除它从内存;你可以更改其属性设置，并使用**打开**方法以后再次打开它。 若要完全消除从内存的对象，请将对象变量设置为*执行任何操作*。  
  
 之前**ActiveConnection**属性设置，则调用**打开**若要创建的实例没有操作数**记录集**通过追加到的字段创建**记录集**[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合。  
  
 如果设置了[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性**adUseClient**，你可以检索以异步方式在两种方式之一的行。 建议的方法是将设置*选项*到**adAsyncFetch**。 或者，可以使用中的"Asynchronous Processing 行集"的动态属性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，但检索到的相关的事件可能会丢失如果未设置*选项*参数**adAsyncFetch**。  
  
> [!NOTE]
>  背景提取 MS 远程提供程序中只能通过支持**打开**方法的*选项*参数。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 某些组合[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)和[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值均无效。 有关哪些选项不能组合的信息，请参阅的主题[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)，和[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [打开和关闭方法的示例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [打开和关闭方法的示例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [打开和关闭方法的示例 （VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [保存和打开方法的示例 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Open 方法 （ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 （ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
