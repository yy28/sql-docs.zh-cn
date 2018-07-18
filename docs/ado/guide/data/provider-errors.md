---
title: 提供程序错误 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a4f551876f97f04f99bd8f2e722cd9e8a89f264
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272336"
---
# <a name="provider-errors"></a>提供程序错误
提供程序错误时，则返回-2147467259 运行时错误。 当你收到此错误时，请检查**错误**的活动的集合**连接**对象，将包含描述所发生的一个或多个错误。  
  
## <a name="the-ado-errors-collection"></a>ADO 错误集合  
 ADO 因为某一特定的 ADO 操作可能会产生多个提供程序错误，公开的通过错误对象的集合**连接**对象。 此集合包含任何对象，如果操作最后成功完成，并包含一个或多个**错误**对象如果出现了问题，提供程序引发了一个或多个错误。 检查每个错误对象，以确定错误的确切原因。  
  
 一旦完成处理已经发生的任何错误后，你可以通过调用来清除集合**清除**方法。 尤其是，务必显式清除**错误**集合，然后才能调用**重新同步**， **UpdateBatch**，或**执行**方法**记录集**对象，**打开**方法**连接**对象，或设置**筛选器**属性**记录集**对象。 通过显式清除该集合，您可以确保任何**错误**从上一个操作不留下集合中的对象。  
  
 某些操作可以生成警告以及错误。 警告也由**错误**中的对象**错误**集合。 当提供程序将警告添加到集合时，它不生成运行时错误。 检查**计数**属性**错误**集合以确定是否由某一特定操作生成一个警告。 如果计数为一个或更高版本，**错误**对象已添加到集合。 一旦你已确定的**错误**集合包含错误或警告，可以循环访问集合，还可以检索有关每项信息**错误**它所包含的对象。 以下简短的 Visual Basic 示例演示这一：  
  
```  
' BeginErrorHandlingVB02  
Private Function DeleteCustomer(ByVal CompanyName As String) As Long  
    On Error GoTo DeleteCustomerError  
  
    rst.Find "CompanyName='" & CompanyName & "'"  
DeleteCustomerError:  
Dim objError As ADODB.Error  
Dim strError As String  
  
    If cnn.Errors.Count > 0 Then  
        For Each objError In cnn.Errors  
            strError = strError & "Error #" & objError.Number & _  
                " " & objError.Description & vbCrLf & _  
                "NativeError: " & objError.NativeError & vbCrLf & _  
                "SQLState: " & objError.SQLState & vbCrLf & _  
                "Reported by: " & objError.Source & vbCrLf & _  
                "Help file: " & objError.HelpFile & vbCrLf & _  
                "Help Context ID: " & objError.HelpContext  
        Next  
        MsgBox strError  
    End If  
End Function  
' EndErrorHandlingVB02  
```  
  
 错误处理例程包括**每个**检查每个对象中的循环**错误**集合。 在此示例中，它将累积，则显示一条消息。 在工作程序中，你将编写代码以执行相应的任务对于每个错误，例如，关闭所有打开的文件和关闭程序中有序的方式。  
  
## <a name="the-error-object"></a>错误对象  
 通过检查**错误**对象，你可以确定发生了什么错误，以及更重要的是，哪些应用程序或哪些对象导致了错误。 **错误**对象具有以下属性：  
  
|属性名称|Description|  
|-------------------|-----------------|  
|**Description**|发生的错误文本说明。|  
|**HelpContext，帮助文件**|是指包含发生的错误的说明的帮助主题和帮助文件。|  
|**NativeError**|提供程序特定的错误数。|  
|**数**|一个长整数，它表示的数字 (列入**ErrorValueEnum**) 的发生的错误。|  
|**数据源**|指示对象或生成了错误的应用程序的名称。|  
|**SQLState**|该提供程序返回的 SQL 语句的过程为五个字符的错误代码。|  
  
 ADO**错误**对象都非常类似于标准的 Visual Basic **Err**对象。 它的属性描述发生的错误。 除了的错误号，您也会收到两个相关的信息片段。 **NativeError**属性包含错误号特定于提供程序正在使用。 在前面的示例中，提供程序是 Microsoft OLE DB Provider for SQL Server，因此**NativeError**将包含特定于 SQL Server 的错误。 **SQLState**属性具有五个字母代码，用于描述 SQL 语句中的错误。  
  
## <a name="event-related-errors"></a>与事件相关的错误  
 **错误**与事件相关的错误发生时，也会使用对象。 你可以确定是否有错误发生的进程中通过检查引发 ADO 事件**错误**对象作为事件参数传递。  
  
 如果成功，结束中引发了事件的操作*adStatus*的事件处理程序的参数将设置为*adStatusOK*。 另一方面，如果引发事件的操作失败， *adStatus*参数设置为*adStatusErrorsOccurred*。 在这种情况下， *pError*参数将包含**错误**描述错误的对象。
