---
title: 提供程序错误 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85d4a7607fae1df7dfb6ec62b8a3bfae8f58001b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924548"
---
# <a name="provider-errors"></a>提供程序错误
提供程序错误时，将返回-2147467259 的一个运行时错误。 当您收到此错误时，检查**错误**活动的集合**连接**对象，它将包含一个或多个描述所发生的错误。  
  
## <a name="the-ado-errors-collection"></a>ADO 错误集合  
 特定的 ADO 操作可能会产生多个提供程序错误，因为 ADO 公开通过错误对象的集合**连接**对象。 此集合包含任何对象，如果操作成功结束，并包含一个或多个**错误**如果出现了问题和提供程序引发了一个或多个错误对象。 检查每个错误对象，以确定错误的确切原因。  
  
 只要有完成处理发生的任何错误，可以通过调用清除集合**清除**方法。 特别是，务必显式清除**错误**集合，然后再调用**重新同步**， **UpdateBatch**，或**CancelBatch**上的方法**记录集**对象，**打开**方法**连接**对象，或者设置**筛选器**属性**记录集**对象。 通过显式清除集合，可以是特定的任何**错误**集合中不留下的对象从上一个操作。  
  
 某些操作可以产生错误的警告。 此外表示警告**错误**中的对象**错误**集合。 当提供程序将警告添加到集合时，它不会生成运行时错误。 检查**计数**的属性**错误**集合以确定是否生成警告时由某一特定操作。 如果计数为一个或更高版本，**错误**对象已添加到集合。 您已确定时，就立即**错误**集合包含错误或警告，您可以循环访问集合并检索每个信息**错误**它所包含的对象。 下面的简短 Visual Basic 示例演示此：  
  
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
  
 错误处理例程包括**为每个**检查每个对象中的循环**错误**集合。 在此示例中，它将显示一条消息。 在处理程序中，可编写代码来执行适当的任务对于每个错误，例如，关闭所有打开的文件和有条理地关闭该程序。  
  
## <a name="the-error-object"></a>错误对象  
 通过检查**错误**对象来确定发生了什么错误，并可更重要的是，哪些应用程序或哪些对象导致了错误。 **错误**对象具有以下属性：  
  
|属性名称|描述|  
|-------------------|-----------------|  
|**说明**|发生的错误的文本说明。|  
|**HelpContext、 HelpFile**|引用包含所发生的错误说明的帮助主题和帮助文件。|  
|**NativeError**|特定于提供程序的错误数。|  
|**数量**|一个长整数，它表示数字 (列入**ErrorValueEnum**) 的发生的错误。|  
|**数据源**|指示生成错误的应用程序的对象的名称。|  
|**SQLState**|在 SQL 语句的过程中的提供程序返回五个字符的错误代码。|  
  
 ADO**错误**对象都非常类似于标准的 Visual Basic **Err**对象。 其属性描述发生的错误。 除了错误号，您还会收到两个相关的信息片段。 **NativeError**属性包含错误号特定于提供程序正在使用。 在上述示例中，提供程序是 Microsoft OLE DB Provider for SQL Server，因此**NativeError**将包含特定于 SQL Server 的错误。 **SQLState**属性具有五个字母的代码，介绍了 SQL 语句中的错误。  
  
## <a name="event-related-errors"></a>与事件相关的错误  
 **错误**与事件相关的错误发生时，也会使用对象。 您可以确定通过检查引发 ADO 事件过程中是否发生了错误**错误**对象作为事件参数传递。  
  
 如果成功，最终会将事件的操作的完成*adStatus*事件处理程序的参数将设置为*adStatusOK*。 另一方面，如果引发该事件的操作不成功， *adStatus*参数设置为*adStatusErrorsOccurred*。 在这种情况下， *pError*参数将包含**错误**描述错误的对象。
