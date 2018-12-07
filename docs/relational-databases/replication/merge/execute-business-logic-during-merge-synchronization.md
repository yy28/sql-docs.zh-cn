---
title: 在合并同步期间执行业务逻辑 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- custom error resolution [SQL Server replication]
- custom change handling [SQL Server replication]
- errors [SQL Server replication], business logic handlers
- merge replication business logic handlers [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
- business logic handlers [SQL Server replication]
ms.assetid: 9d4da2ef-c17f-4a31-a1f6-5c3b7ca85f71
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 083a4ccb00c834fba4f250aa1a2063b76ad9bd86
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52407624"
---
# <a name="execute-business-logic-during-merge-synchronization"></a>在合并同步期间执行业务逻辑
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  通过使用业务逻辑处理程序框架，您可以编写合并同步过程中调用的托管代码程序集。 程序集包括可以响应同步过程中的许多状况的业务逻辑：数据更改、冲突和错误。 业务逻辑处理程序框架提供了一个简单的编程模型，且合并进程提供给程序集的数据的形式是 ADO.NET 数据集，因此可以充分利用了解的 ADO.NET 知识，而不必学习专有接口。 有关如何对业务逻辑处理程序进行编程的详细信息，请参阅：  
  
-   应用程序编程接口 (API) 引用： <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>  
  
-   有关如何实现业务逻辑处理程序的说明：[实现合并项目的业务逻辑处理程序](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
## <a name="uses-for-business-logic-handlers"></a>业务逻辑处理程序用途  
 合并同步进程可以调用业务逻辑处理程序来执行：  
  
-   自定义更改处理  
  
-   自定义冲突解决  
  
-   自定义错误分析  
  
> [!NOTE]  
>  指定的业务逻辑处理程序是针对每个同步的行来执行的， 因此复杂的逻辑以及对其他应用程序或网络服务的调用都可能会影响性能。  
  
### <a name="custom-change-handling"></a>自定义更改处理  
 在处理非冲突数据更改期间可以调用业务逻辑处理程序，它可以执行下列三种操作之一：  
  
-   拒绝数据  
  
     如果应用程序不希望在与给定订阅服务器之间传播更改，这比较有用。 例如，管理员可能会筛选掉不属于订阅服务器分区中的插入操作，也可能拒绝订阅服务器上执行的删除操作。 再如，应用程序可能因库存已不再可用而拒绝订阅服务器上输入的订单。  
  
-   接受数据  
  
     如果应用程序需要先对发布服务器或订阅服务器上所做数据更改进行查看然后再进行传播，这比较有用。 例如，中间层应用程序可能检查从字段输入的新订单，然后与中间层的采购工作流进程集成。  
  
-   应用自定义数据  
  
     如果应用程序需要覆盖特定数据值或操作，这比较有用。 例如，应用程序可能将行删除操作转换为一个特殊的更新操作，将行中 **status** 列的值设置为“已删除”，然后跟踪执行删除操作的客户端的标识。 这对于审核或工作流可能比较有用。  
  
### <a name="custom-conflict-resolution"></a>自定义冲突解决  
 合并复制提供了冲突检测和冲突解决选项，从而允许针对冲突接受默认的解决策略或选择自定义解决。 有关详细信息，请参阅 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)中指定合并项目冲突解决程序。 在处理冲突数据更改期间可以调用业务逻辑处理程序，它可以执行下列两种操作之一：  
  
-   接受默认解决  
  
     如果应用程序可能需要查看冲突、执行其他操作及可能记录自定义冲突日志消息，这比较有用。  
  
-   执行自定义解决  
  
     如果应用程序可能需要选择特定于其业务逻辑的数据值，并需要为同步处理提供此自定义数据集，这比较有用。 例如，应用程序可能通过合并来自发布服务器和订阅服务器数据集的值来提供新版本的入选行。  
  
### <a name="custom-error-resolution"></a>自定义错误分析  
 可以在传播导致出现错误的更改期间调用自定义逻辑。 逻辑可以执行下列两种操作之一：  
  
-   接受默认错误分析  
  
     如果应用程序可能需要查看错误、执行其他操作及可能记录自定义错误日志消息，这比较有用。  
  
-   接受自定义错误分析  
  
     如果应用程序可能需要选择特定于其业务逻辑的数据值，并需要为同步处理提供此自定义数据集，这比较有用。 例如，如果复制过程遇到重复键冲突，业务逻辑处理程序可提供新版本的数据更改，这样就不会再有键冲突。 在发布服务器和订阅服务器上所做的更改就可以保留在数据库中，而复制过程也不必通过删除操作来弥补失败的插入操作。  
  
## <a name="deployment-scenarios-for-business-logic-handlers"></a>业务逻辑处理程序的部署方案  
 可以将业务逻辑处理程序部署于：  
  
-   分发服务器。 使用推送订阅，在分发服务器上执行业务逻辑。  
  
-   订阅服务器。 使用请求订阅，在订阅服务器上执行业务逻辑。  
  
-   Internet 信息服务 (IIS) 服务器（如果使用 Web 同步）。 使用通过 Web 同步来同步的请求订阅，在 IIS 服务器上执行业务逻辑处理程序。  
  
## <a name="see-also"></a>另请参阅  
 [合并复制](../../../relational-databases/replication/merge/merge-replication.md)   
 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)   
 [同步数据](../../../relational-databases/replication/synchronize-data.md)   
 [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
