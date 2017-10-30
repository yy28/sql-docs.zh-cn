---
title: "将发送到 Remote Private Message Queue with the Script Task |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- Script task [Integration Services], remote private message queues
- Message Queue task [Integration Services]
- Script task [Integration Services], examples
ms.assetid: 636314fd-d099-45cd-8bb4-f730d0a06739
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5ab9314ef0825486914d1801bfa2b9613883b43e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="sending-to-a-remote-private-message-queue-with-the-script-task"></a>使用脚本任务向远程私有消息队列发送消息
  消息队列（又称为 MSMQ）使开发人员可以通过发送和接收消息，轻松实现与应用程序之间的快速可靠通信。 消息队列既可位于本地计算机，也可位于远程计算机；既可以是公共的，也可以是私有的。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，MSMQ 连接管理器和消息队列任务不支持向远程计算机上的私有队列发送消息。 但通过使用脚本任务，可轻松地向远程私有队列发送消息。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个包的任务，请考虑以此脚本任务示例中的代码为基础，创建自定义任务。 有关详细信息，请参阅 [开发自定义任务](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>Description  
 下面的示例使用一个现有的 MSMQ 连接管理器，以及对象和方法从 System.Messaging 命名空间，发送到远程私有消息队列某一包变量中包含的文本。 MSMQ 连接管理器的 M:Microsoft.SqlServer.Dts.ManagedConnections.MSMQConn.AcquireConnection(System.Object) 方法调用返回**MessageQueue**对象，其**发送**方法完成此任务。  
  
#### <a name="to-configure-this-script-task-example"></a>配置此脚本任务示例  
  
1.  使用默认名称创建一个 MSMQ 连接管理器。 设置有效远程私有队列的路径，格式如下：  
  
    ```  
    FORMATNAME:DIRECT=OS:<computername>\private$\<queuename>  
    ```  
  
2.  创建[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]变量名为**MessageText**类型的**字符串**要传递到脚本的消息文本。 输入默认消息作为该变量的值。  
  
3.  向设计图面添加一个脚本任务，并对其进行编辑。 上**脚本**选项卡**脚本任务编辑器**，添加`MessageText`变量**ReadOnlyVariables**属性以使该变量可在该脚本.  
  
4.  单击**编辑脚本**以打开[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 脚本编辑器。  
  
5.  脚本项目中添加的引用**System.Messaging**命名空间。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [消息队列任务](../../integration-services/control-flow/message-queue-task.md)  
  
  

