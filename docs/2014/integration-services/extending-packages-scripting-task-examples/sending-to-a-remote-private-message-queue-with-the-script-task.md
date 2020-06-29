---
title: 使用脚本任务向远程私有消息队列发送消息 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], remote private message queues
- Message Queue task [Integration Services]
- Script task [Integration Services], examples
ms.assetid: 636314fd-d099-45cd-8bb4-f730d0a06739
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 65df86efef8e5ffd683e62007d6232bb9067768f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85426434"
---
# <a name="sending-to-a-remote-private-message-queue-with-the-script-task"></a>使用脚本任务向远程私有消息队列发送消息
  消息队列（又称为 MSMQ）使开发人员可以通过发送和接收消息，轻松实现与应用程序之间的快速可靠通信。 消息队列既可位于本地计算机，也可位于远程计算机；既可以是公共的，也可以是私有的。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，MSMQ 连接管理器和消息队列任务不支持向远程计算机上的私有队列发送消息。 但通过使用脚本任务，可轻松地向远程私有队列发送消息。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个包的任务，请考虑以此脚本任务示例中的代码为基础，创建自定义任务。 有关详细信息，请参阅 [开发自定义任务](../extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>说明  
 下面的示例使用一个现有 MSMQ 连接管理器以及 System.Messaging 命名空间的对象和方法，向远程私有消息队列发送包含在包变量中的文本。 对 MSMQ 连接管理器的 M:Microsoft.SqlServer.Dts.ManagedConnections.MSMQConn.AcquireConnection （system.string）方法的调用将返回一个**MessageQueue**对象，其 `Send` 方法完成此任务。  
  
#### <a name="to-configure-this-script-task-example"></a>配置此脚本任务示例  
  
1.  使用默认名称创建一个 MSMQ 连接管理器。 设置有效远程私有队列的路径，格式如下：  
  
    ```  
    FORMATNAME:DIRECT=OS:<computername>\private$\<queuename>  
    ```  
  
2.  创建一个 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 名为**MessageText**的变量 `String` ，以将消息文本传递到脚本。 输入默认消息作为该变量的值。  
  
3.  向设计图面添加一个脚本任务，并对其进行编辑。 在“脚本任务编辑器”的“脚本”选项卡中，将 `MessageText` 变量添加到 ReadOnlyVariables 属性中，使该变量在脚本内可用。  
  
4.  单击“编辑脚本”，打开   Tools for Applications (VSTA) 脚本编辑器[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
5.  在脚本项目中添加对 `System.Messaging` 命名空间的引用。  
  
6.  用下面部分中的代码替换脚本窗口中的内容。  
  
## <a name="code"></a>代码  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.Messaging  
  
Public Class ScriptMain  
  
    Public Sub Main()  
  
        Dim remotePrivateQueue As MessageQueue  
        Dim messageText As String  
  
        remotePrivateQueue = _  
            DirectCast(Dts.Connections("Message Queue Connection Manager").AcquireConnection(Dts.Transaction), _  
            MessageQueue)  
        messageText = DirectCast(Dts.Variables("MessageText").Value, String)  
        remotePrivateQueue.Send(messageText)  
  
        Dts.TaskResult = ScriptResults.Success  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Messaging;  
  
public class ScriptMain  
{  
  
    public void Main()  
        {  
  
            MessageQueue remotePrivateQueue = new MessageQueue();  
            string messageText;  
  
            remotePrivateQueue = (MessageQueue)(Dts.Connections["Message Queue Connection Manager"].AcquireConnection(Dts.Transaction) as MessageQueue);  
            messageText = (string)(Dts.Variables["MessageText"].Value);  
            remotePrivateQueue.Send(messageText);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
```  
  
![Integration Services 图标（小）](../media/dts-16.gif "集成服务图标（小）")**保持与 Integration Services 最**新  <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>另请参阅  
 [消息队列任务](../control-flow/message-queue-task.md)  
  
  
