---
title: 异常消息框编程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- exception message box [SQL Server]
- displaying exception message box
ms.assetid: c771985b-149c-459a-b3cb-7b15fde01150
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8cf02e2759c36ae6408beed0d72b677e130e105a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164107"
---
# <a name="program-exception-message-box"></a>对异常消息框编程
  可以在应用程序中使用异常消息框，以提供更多控制对消息传送所能提供的<xref:System.Windows.Forms.MessageBox>类。 有关详细信息，请参阅[异常消息框编程](../../../2014/database-engine/dev-guide/exception-message-box-programming.md)。 有关如何获取和部署异常消息框.dll 的信息，请参阅[异常消息框应用程序部署](../../../2014/database-engine/dev-guide/deploying-an-exception-message-box-application.md)。  
  
## <a name="procedure"></a>过程  
  
#### <a name="to-handle-an-exception-by-using-the-exception-message-box"></a>通过使用异常消息框处理异常  
  
1.  将托管代码项目中的某个引用添加到 Microsoft.ExceptionMessageBox.dll 程序集。  
  
2.  （可选）添加`using`(C#) 或`Imports`([!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic.NET) 指令以使用<xref:Microsoft.SqlServer.MessageBox>命名空间。  
  
3.  创建 try-catch 块处理预期异常。  
  
4.  内`catch`块中，创建的实例<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>类。 传递<xref:System.Exception>处理对象`try` - `catch`块。  
  
5.  （可选）设置一个或多个以下属性上<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 枚举，用于指定要在异常消息框中显示的按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 枚举，用于指定异常消息框的默认按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 用于控制异常消息框的其他行为的枚举。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 枚举，用于指定要在异常消息框中显示的符号。  
  
6.  调用 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 传递异常消息框所属的父窗口。  
  
7.  （可选）记下的值返回<xref:System.Windows.Forms.DialogResult>枚举，如果您需要确定哪个按钮用户单击。  
  
#### <a name="to-display-the-exception-message-box-without-an-exception"></a>显示没有异常的异常消息框  
  
1.  将托管代码项目中的某个引用添加到 Microsoft.ExceptionMessageBox.dll 程序集。  
  
2.  （可选）添加`using`(C#) 或`Imports`(Visual Basic.NET) 指令以使用<xref:Microsoft.SqlServer.MessageBox>命名空间。  
  
3.  创建 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 类的实例。 将消息文本为<xref:System.String>值。  
  
4.  （可选）设置一个或多个以下属性上<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 枚举，用于指定要在异常消息框中显示的按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Caption%2A> - 异常消息框的对话框标题。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 枚举，用于指定异常消息框对话框的默认按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 用于控制异常消息框的其他行为的枚举。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 枚举，用于指定要在异常消息框中显示的符号。  
  
5.  调用 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 传递异常消息框所属的父窗口。  
  
6.  （可选）记下所返回的值<xref:System.Windows.Forms.DialogResult>枚举，如果您需要确定哪个按钮用户单击。  
  
#### <a name="to-display-the-exception-message-box-with-customized-buttons"></a>显示具有自定义按钮的异常消息框  
  
1.  将托管代码项目中的某个引用添加到 Microsoft.ExceptionMessageBox.dll 程序集。  
  
2.  （可选）添加`using`(C#) 或`Imports`(Visual Basic.NET) 指令以使用<xref:Microsoft.SqlServer.MessageBox>命名空间。  
  
3.  按以下两种方式之一创建 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 类的实例：  
  
    -   传递<xref:System.Exception>处理对象`try` - `catch`块。  
  
    -   将消息文本为<xref:System.String>值。  
  
4.  设置为下列任一值<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.AbortRetryIgnore> -显示**中止**，**重试**，并**忽略**按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.Custom> -显示自定义按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OK> -显示**确定**按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OKCancel> -显示**确定**并**取消**按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.RetryCancel> -显示**重试**并**取消**按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNo> -显示**是**并**否**按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNoCancel> -显示**是**，**否**，并**取消**按钮。  
  
5.  （可选）如果使用自定义按钮，调用的重载之一<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.SetButtonText%2A>方法，以指定最多五个自定义按钮文本。  
  
6.  调用 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 传递异常消息框所属的父窗口。  
  
7.  （可选）记下所返回的值<xref:System.Windows.Forms.DialogResult>枚举，如果您需要确定哪个按钮用户单击。 如果使用自定义按钮，记下的值<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDialogResult>为<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CustomDialogResult%2A>属性来确定自定义按钮用户单击。  
  
#### <a name="to-allow-users-to-decide-whether-to-show-the-exception-message-box"></a>允许用户决定是否要显示异常消息框  
  
1.  将托管代码项目中的某个引用添加到 Microsoft.ExceptionMessageBox.dll 程序集。  
  
2.  （可选）添加`using`(C#) 或`Imports`(Visual Basic.NET) 指令以使用<xref:Microsoft.SqlServer.MessageBox>命名空间。  
  
3.  按以下两种方式之一创建 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 类的实例：  
  
    -   传递<xref:System.Exception>处理对象`try` - `catch`块。  
  
    -   将消息文本为<xref:System.String>值。  
  
4.  设置<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.ShowCheckbox%2A>属性设置为`true`。  
  
5.  （可选）指定的文本，要求用户来决定是否显示异常消息框中的再次为<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxText%2A>。 默认文本为“不再显示此消息”。  
  
6.  如果需要保留用户的决定仅对应用程序的执行期间，将的值设置<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.IsCheckboxChecked%2A>为全局<xref:System.Boolean>变量。 在创建异常消息框的实例前计算此值。  
  
7.  如果需要永久存储用户的决定，请执行以下操作：  
  
    1.  调用 CreateSubKey 方法以打开自定义注册表项的应用程序使用，并将设置<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryKey%2A>到返回的 RegistryKey 对象。  
  
    2.  将 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryValue%2A> 设置为使用的注册表值的名称。  
  
    3.  设置<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryMeansDoNotShowDialog%2A>到`true`。  
  
    4.  调用 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 计算指定的注册表项，仅当注册表项中存储的数据为 0 时才显示异常消息框。 如果显示对话框且用户在单击按钮前选中复选框，则注册表项中的数据设置为 1。  
  
## <a name="example"></a>示例  
 此示例使用异常消息框，其唯一**确定**按钮以显示从应用程序异常，包括处理的异常以及其他特定于应用程序的信息的信息。  
  
 [!code-csharp[HowTo#emb_showOKbutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showokbutton)]  
  
 [!code-vb[HowTo#emb_vb_showOKbutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showokbutton)]  
  
## <a name="example"></a>示例  
 此示例使用具有异常消息框**是**并**否**中供用户选择的按钮。  
  
 [!code-csharp[HowTo#emb_showYesNobutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showyesnobutton)]  
  
 [!code-vb[HowTo#emb_vb_showYesNobutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showyesnobutton)]  
  
## <a name="example"></a>示例  
 以下示例使用具有自定义按钮的异常消息框。  
  
 [!code-csharp[HowTo#emb_showcustombutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showcustombutton)]  
  
 [!code-vb[HowTo#emb_vb_showcustombutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showcustombutton)]  
  
## <a name="example"></a>示例  
 以下示例使用复选框来确定是否显示异常消息框。  
  
 [!code-csharp[HowTo#emb_usecheckbox](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_usecheckbox)]  
  
 [!code-vb[HowTo#emb_vb_usecheckbox](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_usecheckbox)]  
  
## <a name="example"></a>示例  
 以下示例使用复选框和注册表项来确定是否显示异常消息框。  
  
 [!code-csharp[HowTo#emb_useregkey](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_useregkey)]  
  
 [!code-vb[HowTo#emb_vb_useregkey](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_useregkey)]  
  
## <a name="example"></a>示例  
 以下示例使用异常消息框来显示对排除故障或调试有帮助的其他信息。  
  
 [!code-csharp[HowTo#emb_moreinfo](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_moreinfo)]  
  
 [!code-vb[HowTo#emb_vb_moreinfo](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_moreinfo)]  
  
  
