---
title: ADO 事件处理程序摘要 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- event handlers [ADO]
ms.assetid: b34f4472-5e04-4a2c-ab64-38d6eca31a69
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08a9f6ba0f81c1818125bd38d5c66097c21971de
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="ado-connection-and-recordset-events"></a>ADO 连接和记录集事件
两个 ADO 对象可以引发事件：[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象和[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 **ConnectionEvent**系列与操作上**连接**对象，与**RecordsetEvent**系列与操作上**记录集**对象。

-   **连接事件**： 在连接上的事务开始，也会提交，或者返回; 当将会回滚时，将发出事件[命令](../../../ado/reference/ado-api/command-object-ado.md)执行; 期间出现警告时**连接事件**操作;时，或者当**连接**开始或结束。

-   **记录集事件**： 围绕异步读取操作以及当你的各行之间导航时发出事件**记录集**对象，请更改的行中的字段**记录集**，更改中的行**记录集**，打开**记录集**与服务器端游标，关闭**记录集**，或进行任何更改在任何**记录集**。

 下表汇总了事件及其说明。

|ConnectionEvent|Description|
|---------------------|-----------------|
|[BeginTransComplete，CommitTransComplete，RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**事务管理**-通知连接上的当前事务已启动、 提交或回滚。|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)， [ConnectComplete，断开连接](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**连接管理**-通知当前的连接将开始，已启动，或已结束。|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)， [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**命令执行管理**-连接上的当前命令的执行将启动或已结束的通知。|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**信息性**-没有有关当前操作的其他信息的通知。|

|RecordsetEvent|Description|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)， [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**检索状态**-数据检索操作的进度通知或检索操作已完成。 这些事件才可用如果**记录集**使用客户端游标已打开。|
|[WillChangeField FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**字段更改管理**-当前字段的值将更改或已更改的通知。|
|[WillMove、 MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)， [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**导航管理**-当前行位置中的通知**记录集**将更改、 已更改，或已达到末尾**记录集**。|
|[WillChangeRecord RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**行更改管理**-通知的当前行中的该内容**记录集**会更改，或已更改。|
|[WillChangeRecordset RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**记录集更改管理**-这是在当前的通知**记录集**会更改，或已更改。|

## <a name="see-also"></a>另请参阅
 [通过语言的 ADO 事件实例化](../../../ado/guide/data/ado-event-instantiation-by-language.md) [ADO 事件](../../../ado/reference/ado-api/ado-events.md)[事件参数](../../../ado/guide/data/event-parameters.md)[事件处理程序是如何协同工作](../../../ado/guide/data/how-event-handlers-work-together.md)[的事件类型](../../../ado/guide/data/types-of-events.md)
