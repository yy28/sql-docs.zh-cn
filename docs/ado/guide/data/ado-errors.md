---
title: ADO 错误 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4fadb19aac4700738f4c6ec43449b3de7d4a4a18
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47776365"
---
# <a name="ado-run-time-errors"></a>ADO 运行时错误
ADO 错误报告到你的程序为运行时错误。 您的编程语言的错误捕获机制可用于捕获并处理它们。 例如，在 Visual Basic 中，使用**On Error**语句。 在 Visual c + +，这取决于您用来访问 ADO 库的方法。 借助 #import，使用**try catch**块。 否则，需要显式检索错误对象通过调用 c + + 程序员**GetErrorInfo**。 下面的 Visual Basic sub 过程演示了捕获 ADO 错误：

```
' BeginErrorHandlingVB01
Private Sub Form_Load()
' Turn on error handling
On Error GoTo FormLoadError

'Open the database and the recordset for processing.
'
Dim strCnn As String
strCnn = "Provider=sqloledb;" & _
    "Data Source=a-iresmi2000;" & _
    "Initial Catalog=Northwind;Integrated Security=SSPI"

' cnn is a Public Connection Object because
' it was defined WithEvents
Set cnn = New ADODB.Connection
cnn.Open strCnn

' The next line of code intentionally causes
' an error by trying to open a connection
' that has already been opened.
cnn.Open strCnn

' rst is a Public Recordset because it
' was defined WithEvents
Set rst = New ADODB.Recordset
rst.Open "Customers", cnn

Exit Sub

' Error handler
FormLoadError:
    Dim strErr As String
    Select Case Err
        Case adErrObjectOpen
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            strErr = strErr & "Error reported by: " & Err.Source & vbCrLf
            strErr = strErr & "Help File: " & Err.HelpFile & vbCrLf
            strErr = strErr & "Topic ID: " & Err.HelpContext
            MsgBox strErr
            Debug.Print strErr
            Err.Clear
            Resume Next
        ' If some other error occurs that
        ' has nothing to do with ADO, show
        ' the number and description and exit.
        Case Else
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            MsgBox strErr
            Debug.Print strErr
            Unload Me
    End Select
End Sub
' EndErrorHandlingVB01
```

 这**Form_Load**事件过程有意创建一条错误通过尝试打开相同**连接**两次对象。 第二次**打开**方法调用时，会激活错误处理程序。 在这种情况下错误属于类型**adErrObjectOpen**，因此恢复程序执行之前，错误处理程序将显示以下消息：

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 错误消息中包含每条信息提供的 Visual Basic **Err**对象除**调用**值，该值在此处不适用。 错误编号会通知你哪些错误。 该说明仅在其中不想要自己处理错误的情况下很有用。 只需，可以将其传递到用户。 尽管通常需要使用自定义应用程序的消息，不能预测每个错误;说明提供有关发生的问题的一些线索。 在示例代码中，通过报告了错误**连接**对象。 你将看到对象的类型或以编程方式 ID 此处 — 不是变量的名称。

> [!NOTE]
>  Visual Basic **Err**对象仅包含有关最新的错误的信息。 ADO**错误**系列**连接**对象都包含一个**错误**引发的最新的 ADO 操作每个错误的对象。 使用**错误**集合而不是**Err**对象以处理多个错误。 有关详细信息**错误**集合，请参阅[提供程序错误](../../../ado/guide/data/provider-errors.md)。 但是，如果没有有效**连接**对象， **Err**对象是 ADO 错误的信息的唯一源。

 哪些类型的操作有可能导致 ADO 错误？ 常见的 ADO 错误可能涉及到如打开对象**连接**或**记录集**、 尝试更新数据，或调用方法或您的提供程序不支持的属性。

 OLE DB 错误也可以传递到您的应用程序中的运行时错误**错误**集合。

 以下主题提供 ADO 错误详细信息。

-   [ADO 错误参考](../../../ado/guide/data/ado-error-reference.md)
