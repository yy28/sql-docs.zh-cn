---
title: 异常消息框编程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- exception message box [SQL Server]
- displaying exception message box
ms.assetid: c771985b-149c-459a-b3cb-7b15fde01150
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 316afc6d5f3a87ff7431240681066ac5ee66ede6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62780689"
---
# <a name="program-exception-message-box"></a>对异常消息框编程
  可以使用应用程序中的异常消息框，它与 <xref:System.Windows.Forms.MessageBox> 类相比，可以大大提高对消息传送的控制。 有关详细信息，请参阅[异常消息框编程](../../../2014/database-engine/dev-guide/exception-message-box-programming.md)。 有关如何获取和部署异常消息框 .dll 的信息，请参阅 [Deploying an Exception Message Box Application](../../../2014/database-engine/dev-guide/deploying-an-exception-message-box-application.md)。  
  
## <a name="procedure"></a>过程  
  
#### <a name="to-handle-an-exception-by-using-the-exception-message-box"></a>通过使用异常消息框处理异常  
  
1.  将托管代码项目中的某个引用添加到 Microsoft.ExceptionMessageBox.dll 程序集。  
  
2.  （可选）添加`using`(C#) 或`Imports`([!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic.NET) 指令以使用<xref:Microsoft.SqlServer.MessageBox>命名空间。  
  
3.  创建 try-catch 块处理预期异常。  
  
4.  在 `catch` 块中，创建 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 类的实例。 传递<xref:System.Exception>处理对象`try` - `catch`块。  
  
5.  （可选）为 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 设置下列一个或多个属性：  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 枚举，用于指定要在异常消息框中显示的按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 枚举，用于指定异常消息框的默认按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 用于控制异常消息框的其他行为的枚举。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 枚举，用于指定要在异常消息框中显示的符号。  
  
6.  调用 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 传递异常消息框所属的父窗口。  
  
7.  （可选）记下的值返回<xref:System.Windows.Forms.DialogResult>枚举，如果您需要确定哪个按钮用户单击。  
  
#### <a name="to-display-the-exception-message-box-without-an-exception"></a>显示没有异常的异常消息框  
  
1.  将托管代码项目中的某个引用添加到 Microsoft.ExceptionMessageBox.dll 程序集。  
  
2.  （可选）添加`using`(C#) 或`Imports`(Visual Basic.NET) 指令以使用<xref:Microsoft.SqlServer.MessageBox>命名空间。  
  
3.  创建 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 类的实例。 将消息文本作为 <xref:System.String> 值传递。  
  
4.  （可选）为 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 设置下列一个或多个属性：  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 枚举，用于指定要在异常消息框中显示的按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Caption%2A> - 异常消息框的对话框标题。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 枚举，用于指定异常消息框对话框的默认按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 用于控制异常消息框的其他行为的枚举。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 枚举，用于指定要在异常消息框中显示的符号。  
  
5.  调用 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 传递异常消息框所属的父窗口。  
  
6.  （可选）如果需要确定用户单击的按钮，请注明返回的 <xref:System.Windows.Forms.DialogResult> 枚举值。  
  
#### <a name="to-display-the-exception-message-box-with-customized-buttons"></a>显示具有自定义按钮的异常消息框  
  
1.  将托管代码项目中的某个引用添加到 Microsoft.ExceptionMessageBox.dll 程序集。  
  
2.  （可选）添加`using`(C#) 或`Imports`(Visual Basic.NET) 指令以使用<xref:Microsoft.SqlServer.MessageBox>命名空间。  
  
3.  按以下两种方式之一创建 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 类的实例：  
  
    -   传递<xref:System.Exception>处理对象`try` - `catch`块。  
  
    -   将消息文本作为 <xref:System.String> 值传递。  
  
4.  为 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> 设置以下值之一：  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.AbortRetryIgnore> -显示**中止**，**重试**，并**忽略**按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.Custom> - 显示自定义按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OK> -显示**确定**按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OKCancel> -显示**确定**并**取消**按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.RetryCancel> -显示**重试**并**取消**按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNo> -显示**是**并**否**按钮。  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNoCancel> -显示**是**，**否**，并**取消**按钮。  
  
5.  （可选）如果使用自定义按钮，请调用 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.SetButtonText%2A> 方法的重载之一以指定最多五个自定义按钮的文本。  
  
6.  调用 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 方法。 传递异常消息框所属的父窗口。  
  
7.  （可选）如果需要确定用户单击的按钮，请注明返回的 <xref:System.Windows.Forms.DialogResult> 枚举值。 如果使用自定义按钮，请注明 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDialogResult> 属性的 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CustomDialogResult%2A> 值以确定用户单击的自定义按钮。  
  
#### <a name="to-allow-users-to-decide-whether-to-show-the-exception-message-box"></a>允许用户决定是否要显示异常消息框  
  
1.  将托管代码项目中的某个引用添加到 Microsoft.ExceptionMessageBox.dll 程序集。  
  
2.  （可选）添加`using`(C#) 或`Imports`(Visual Basic.NET) 指令以使用<xref:Microsoft.SqlServer.MessageBox>命名空间。  
  
3.  按以下两种方式之一创建 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 类的实例：  
  
    -   传递<xref:System.Exception>处理对象`try` - `catch`块。  
  
    -   将消息文本作为 <xref:System.String> 值传递。  
  
4.  将 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.ShowCheckbox%2A> 属性设置为 `true`。  
  
5.  （可选）指定请用户决定以后是否还为 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxText%2A> 显示异常消息框的文本。 默认文本为“不再显示此消息”。  
  
6.  如果需要仅在应用程序执行期间保留用户的决定，请将 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.IsCheckboxChecked%2A> 的值设置为全局 <xref:System.Boolean> 变量。 在创建异常消息框的实例前计算此值。  
  
7.  如果需要永久存储用户的决定，请执行以下操作：  
  
    1.  调用 CreateSubKey 方法以打开你的应用程序使用的自定义注册表项，然后将 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryKey%2A> 设置为返回的 RegistryKey 对象。  
  
    2.  将 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryValue%2A> 设置为使用的注册表值的名称。  
  
    3.  将 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryMeansDoNotShowDialog%2A> 设置为 `true`。  
  
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
  
  
