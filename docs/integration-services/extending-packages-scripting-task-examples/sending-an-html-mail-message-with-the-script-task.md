---
title: "发送 HTML 邮件 with the Script Task |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Send Mail task [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], HTML mail message
ms.assetid: dd2b1eef-b04f-4946-87ab-7bc56bb525ce
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: b5f50a79ca83243ea130c77a0d95ab402ba2d31a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="sending-an-html-mail-message-with-the-script-task"></a>使用脚本任务发送 HTML 邮件消息
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] SendMail 任务仅支持纯文本格式的邮件消息。 但是，您可以使用脚本任务以及 .NET Framework 的邮件功能轻松发送 HTML 邮件消息。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个包的任务，请考虑以此脚本任务示例中的代码为基础，创建自定义任务。 有关详细信息，请参阅 [开发自定义任务](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>Description  
 下面的示例使用**System.Net.Mail**命名空间配置并发送 HTML 邮件消息。 脚本获取收件人、 主题和从包变量的电子邮件正文中，使用它们来创建一个新**MailMessag**e，并设置其**IsBodyHtml**属性**True**。 然后它从另一个包变量初始化的实例中获取 SMTP 服务器名称**System.Net.Mail.SmtpClient**，并调用其**发送**方法发送 HTML 消息。 该示例将消息发送功能封装到一个可在其他脚本中重用的子例程中。  
  
#### <a name="to-configure-this-script-task-example-without-an-smtp-connection-manager"></a>不使用 SMTP 连接管理器配置此脚本任务示例  
  
1.  创建名为 `HtmlEmailTo`、`HtmlEmailFrom` 和 `HtmlEmailSubject` 的字符串变量，并向它们分配相应的值，以用于有效的测试消息。  
  
2.  创建一个名为 `HtmlEmailBody` 的字符串变量，并向其分配 HTML 标记字符串。 例如：  
  
    ```  
    <html><body><h1>Testing</h1><p>This is a <b>test</b> message.</p></body></html>  
    ```  
  
3.  创建一个名为 `HtmlEmailServer` 的字符串变量，并向其分配一个可接收匿名传出消息的可用 SMTP 服务器的名称。  
  
4.  分配到这些变量的所有五个**ReadOnlyVariables**新的脚本任务的属性。  
  
5.  导入**System.Net**和**System.Net.Mail**到你的代码的命名空间。  
  
 本主题中的示例代码从包变量获取 SMTP 服务器名称。 当然，还可以利用 SMTP 连接管理器封装连接信息，并在代码中从连接管理器提取服务器名称。 SMTP 连接管理器的 <xref:Microsoft.SqlServer.Dts.ManagedConnections.SMTPConn.AcquireConnection%2A> 方法以下列格式返回一个字符串：  
  
 `SmtpServer=smtphost;UseWindowsAuthentication=False;EnableSsl=False;`  
  
 你可以使用**String.Split**方法可以转换为在每个分号 （;） 的各个字符串数组将此自变量列表或等于号 （=），然后从和提取第二个参数 （下标 1） 作为服务器名称数组。  
  
#### <a name="to-configure-this-script-task-example-with-an-smtp-connection-manager"></a>使用 SMTP 连接管理器配置此脚本任务示例  
  
1.  修改脚本任务通过删除之前配置`HtmlEmailServer`变量的列表从**ReadOnlyVariables**。  
  
2.  将获取服务器名称的代码行：  
  
    ```  
    Dim smtpServer As String = _  
      Dts.Variables("HtmlEmailServer").Value.ToString  
    ```  
  
     替换为以下代码行：  
  
    ```  
    Dim smtpConnectionString As String = _  
      DirectCast(Dts.Connections("SMTP Connection Manager").AcquireConnection(Dts.Transaction), String)  
    Dim smtpServer As String = _  
      smtpConnectionString.Split(New Char() {"="c, ";"c})(1)  
    ```  
  
## <a name="code"></a>代码  
  
```vb  
Public Sub Main()  
  
  Dim htmlMessageTo As String = _  
    Dts.Variables("HtmlEmailTo").Value.ToString  
  Dim htmlMessageFrom As String = _  
    Dts.Variables("HtmlEmailFrom").Value.ToString  
  Dim htmlMessageSubject As String = _  
    Dts.Variables("HtmlEmailSubject").Value.ToString  
  Dim htmlMessageBody As String = _  
    Dts.Variables("HtmlEmailBody").Value.ToString  
  Dim smtpServer As String = _  
    Dts.Variables("HtmlEmailServer").Value.ToString  
  
  SendMailMessage( _  
      htmlMessageTo, htmlMessageFrom, _  
      htmlMessageSubject, htmlMessageBody, _  
      True, smtpServer)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
  
Private Sub SendMailMessage( _  
    ByVal SendTo As String, ByVal From As String, _  
    ByVal Subject As String, ByVal Body As String, _  
    ByVal IsBodyHtml As Boolean, ByVal Server As String)  
  
  Dim htmlMessage As MailMessage  
  Dim mySmtpClient As SmtpClient  
  
  htmlMessage = New MailMessage( _  
    SendTo, From, Subject, Body)  
  htmlMessage.IsBodyHtml = IsBodyHtml  
  
  mySmtpClient = New SmtpClient(Server)  
  mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials  
  mySmtpClient.Send(htmlMessage)  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            string htmlMessageTo = Dts.Variables["HtmlEmailTo"].Value.ToString();  
            string htmlMessageFrom = Dts.Variables["HtmlEmailFrom"].Value.ToString();  
            string htmlMessageSubject = Dts.Variables["HtmlEmailSubject"].Value.ToString();  
            string htmlMessageBody = Dts.Variables["HtmlEmailBody"].Value.ToString();  
            string smtpServer = Dts.Variables["HtmlEmailServer"].Value.ToString();  
  
            SendMailMessage(htmlMessageTo, htmlMessageFrom, htmlMessageSubject, htmlMessageBody, true, smtpServer);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
        private void SendMailMessage(string SendTo, string From, string Subject, string Body, bool IsBodyHtml, string Server)  
        {  
  
            MailMessage htmlMessage;  
            SmtpClient mySmtpClient;  
  
            htmlMessage = new MailMessage(SendTo, From, Subject, Body);  
            htmlMessage.IsBodyHtml = IsBodyHtml;  
  
            mySmtpClient = new SmtpClient(Server);  
            mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials;  
            mySmtpClient.Send(htmlMessage);  
  
        }  
```  
  
## <a name="see-also"></a>另請參閱  
 [发送邮件任务](../../integration-services/control-flow/send-mail-task.md)  
  
  

