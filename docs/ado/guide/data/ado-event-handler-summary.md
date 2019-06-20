---
title: ADO 事件处理程序摘要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- event handlers [ADO]
ms.assetid: b34f4472-5e04-4a2c-ab64-38d6eca31a69
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f1901892b3e48446f3598b24ebb0a529360b9edf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702642"
---
# <a name="ado-connection-and-recordset-events"></a>ADO 连接和记录集事件
两个 ADO 对象可以引发事件：[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象和[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 **ConnectionEvent**上与操作相关系列**连接**对象，并**RecordsetEvent**系列上与操作相关**记录集**对象。

-   **连接事件**:在连接上的事务开始、 已提交，或回滚; 时，将发出事件当[命令](../../../ado/reference/ado-api/command-object-ado.md)执行; 期间出现警告时**连接事件**操作; 或者当**连接**开始或结束。

-   **记录集事件**:围绕异步读取操作以及的各行之间导航时发出的事件**记录集**对象，请更改的行中的字段**记录集**，更改行中的**记录集**，打开**记录集**与服务器端游标，关闭**记录集**，或进行任何更改都在**记录集**。

 下表汇总了事件及其说明。

|ConnectionEvent|Description|
|---------------------|-----------------|
|[BeginTransComplete，CommitTransComplete，RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**事务管理**-启动连接的当前事务后，通知已提交或回滚。|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)， [ConnectComplete，断开连接](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**连接管理**-通知的当前连接将启动，启动后，或已结束。|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)， [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**命令执行管理**-通知的连接上的当前命令执行将开始或已结束。|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**信息性**-通知将有关当前操作的其他信息。|

|RecordsetEvent|Description|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)， [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**检索状态**-通知进度的数据检索操作，或检索操作完成后。 这些事件才可用如果**记录集**使用客户端游标已打开。|
|[WillChangeField FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**字段更改管理**-当前字段的值将发生更改，或已更改的通知。|
|[WillMove、 MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)， [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**导航管理**的当前行位置中的通知**记录集**将更改、 已更改，或已达到末尾**记录集**。|
|[WillChangeRecord RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**行更改管理**-通知的当前行中的内容**记录集**将发生更改，或已更改。|
|[WillChangeRecordset RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**记录集更改管理**-某些内容在当前通知**记录集**将发生更改，或已更改。|

## <a name="see-also"></a>请参阅
 [ADO 事件实例化的语言](../../../ado/guide/data/ado-event-instantiation-by-language.md) [ADO 事件](../../../ado/reference/ado-api/ado-events.md)[事件参数](../../../ado/guide/data/event-parameters.md)[事件处理程序如何协同工作](../../../ado/guide/data/how-event-handlers-work-together.md)[的事件类型](../../../ado/guide/data/types-of-events.md)
