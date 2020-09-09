---
description: WMI Provider for Server Events 类和属性
title: WMI Provider for Server Events 类和属性
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- event classes [WMI]
- WMI Provider for Server Events, events listed
- classes [WMI]
ms.assetid: e2916cd7-a3ed-41e6-97b4-2ee060754cbe
author: markingmyname
ms.author: maghan
ms.openlocfilehash: be17f5425d66956028fce13144b6bb908230fca9
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542727"
---
# <a name="wmi-provider-for-server-events-classes-and-properties"></a>WMI Provider for Server Events 类和属性
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  以下服务器事件构成了 WMI Provider for Server Events 的编程模型。 通过针对提供程序发出 WQL 查询，可以对两种主要的事件类别进行查询。 它们分别是数据定义语言 (DDL) 事件和跟踪事件。 还可以查询 QUEUE_ACTIVATION 和 BROKER_QUEUE_DISABLED Service Broker 事件。 请注意以下树形关系图中的内在关系。 例如，DDL_ASSEMBLY_EVENTS 事件包括任意 ALTER_ASSEMBLY、CREATE_ASSEMBLY 和 DROP_ASSEMBLY 事件。 同样，TRC_FULL_TEXT 事件包括任意 FT_CRAWL_ABORTED、FT_CRAWL_STARTED 和 FT_CRAWL_STOPPED 事件。 ALL_EVENTS 包括所有 DDL 事件、跟踪事件、QUEUE_ACTIVATION 和 BROKER_QUEUE_DISABLED。  
  
 若要了解可以通过事件或事件组查询的属性，请参考事件架构。 默认情况下，事件架构安装在以下目录中：[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd。  
  
 或者，您可以引用在处发布的事件架构 [https://schemas.microsoft.com/sqlserver](https://go.microsoft.com/fwlink/?linkid=43100) 。  
  
 例如，通过引用 ALTER_DATABASE 事件，您将了解其父事件 DDL_SERVER_LEVEL_EVENTS，其属性为 **TSQLCommand** 和 **DatabaseName**。 此事件还继承属性 **SQLInstance**、 **PostTime**、 **ComputerName**、 **SPID**和 **LoginName**。 该事件没有子事件。  
  
> [!NOTE]  
>  执行 DDL 式操作的系统存储过程还可以激发事件通知。 测试您的事件通知以确定它们是否响应运行的系统存储过程。 例如，CREATE TYPE 语句和 **sp_addtype** 存储过程都将激发在 CREATE_TYPE 事件上创建的事件通知。 有关详细信息，请参阅 [DDL 事件](../../relational-databases/triggers/ddl-events.md)。  
  
 **数据定义语言事件和事件组**  
  
 ![WMI Provider for Server Events 事件树](../../relational-databases/wmi-provider-server-events/media/sql-wmi-ddl-events-ktm.gif "WMI Provider for Server Events 事件树")  
  
 **跟踪事件和事件组**  
  
 ![跟踪事件和事件组](../../relational-databases/wmi-provider-server-events/media/sql-wmi-trc-all-events.gif "跟踪事件和事件组")  
  
## <a name="see-also"></a>另请参阅  
 [WMI Provider for Server Events 的概念](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)   
 [将 WQL 与 WMI Provider for Server Events 结合使用](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)  
  
  
