---
title: MSMQ 连接管理器编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msmqconnectionmanager.f1
helpviewer_keywords:
- MSMQ Connection Manager Editor
ms.assetid: ef842cb4-82da-4550-85fe-9bedbc1e77c7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4d407cc3c0324b80ff63484f4e7c39ea30575ebc
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967037"
---
# <a name="msmq-connection-manager-editor"></a>MSMQ 连接管理器编辑器
  可以使用“MSMQ 连接管理器”对话框指定“消息队列”（也称为 MSMQ）消息队列的路径。****  
  
 若要了解有关 MSMQ 连接管理器的详细信息，请参阅 [MSMQ Connection Manager](connection-manager/msmq-connection-manager.md)。  
  
> [!NOTE]  
>  MSMQ 连接管理器支持本地公共队列、本地专用队列和远程公共队列。 它不支持远程专用队列。 有关使用脚本任务的解决方法，请参阅 [向远程私有消息队列使用脚本任务发送](control-flow/script-task.md)。  
  
## <a name="options"></a>选项  
 **名称**  
 为工作流中的 MSMQ 连接管理器提供唯一的名称。 所提供的名称将在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中显示。  
  
 **说明**  
 描述连接管理器。 最好按照连接管理器的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
 **路径**  
 键入消息队列的完整路径。 路径的格式取决于队列的类型。  
  
|队列类型|示例路径|  
|----------------|-----------------|  
|公用|\<computer name>\\<队列名称\>|  
|Private|\<computer name>\Private $ \\<队列名称\>|  
  
 可以用“.”代表本地计算机。  
  
 **测试**  
 在配置 MSMQ 连接管理器之后，单击“测试”确定该连接是否可用。****  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
