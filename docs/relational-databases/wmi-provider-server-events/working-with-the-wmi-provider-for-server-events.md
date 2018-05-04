---
title: 使用 WMI Provider for Server Events |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- event notifications [WMI]
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- Service Broker [WMI]
- WMI Provider for Server Events, connection strings
- WMI Provider for Server Events, Service Broker
- notifications [WMI]
- WMI Provider for Server Events, security
ms.assetid: cd974b3b-2309-4a20-b9be-7cfc93fc4389
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 555b5a0024810c3d9cb7ecd3baa562072f97f483
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-the-wmi-provider-for-server-events"></a>使用 WMI Provider for Server Events
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  本主题为您提供在使用 WMI Provider for Server Events 编程前应考虑的一些准则。  
  
## <a name="enabling-service-broker"></a>启用 Service Broker  
 WMI Provider for Server Events 通过将事件的 WQL 查询转换为目标数据库中的事件通知而发挥作用。 在针对提供程序编程时，了解事件通知的工作方式可能对您很有用。 有关详细信息，请参阅 [WMI Provider for Server Events 的概念](http://technet.microsoft.com/library/ms180560.aspx)。  
  
 特别是由于 WMI 提供程序创建的事件通知使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来发送有关服务器事件的消息，因此只要生成事件就必须启用此服务。 如果您的程序查询服务器实例的事件，必须启用该实例的 msdb 中的 [!INCLUDE[ssSB](../../includes/sssb-md.md)]，因为这是提供程序所创建的目标 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 服务（名为 SQL/Notifications/ProcessWMIEventProviderNotification/v1.0）的位置。 如果您的程序查询数据库或特定数据库对象中的事件，必须启用该目标数据库中的 [!INCLUDE[ssSB](../../includes/sssb-md.md)]。 如果在部署应用程序后未启用相应的 [!INCLUDE[ssSB](../../includes/sssb-md.md)]，会将基础事件通知所生成的任意事件发送到事件通知使用的服务队列，但是在启用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 之前不返回给 WMI 管理应用程序。  
  
 以下查询确定在服务器实例上启用的 Service Broker 和 Broker 实例 GUID：  
  
```  
SELECT name, is_broker_enabled, service_broker_guid FROM sys.databases;  
```  
  
 msdb 的 Service Broker GUID 特别值得关注，因为这是提供程序目标服务的位置。  
  
 若要启用[!INCLUDE[ssSB](../../includes/sssb-md.md)]在数据库中，使用的 ENABLE_BROKER 设置选项[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)语句。  
  
## <a name="specifying-a-connection-string"></a>指定连接字符串  
 应用程序通过连接到 WMI Provider for Server Events 所定义的 WMI 命名空间，将该提供程序定向到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 Windows WMI 服务将此命名空间映射到提供程序 DLL Sqlwep.dll 并将其加载到内存。 每个实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有其自己的 WMI 命名空间，默认值为： \\ \\。\\*根*\Microsoft\SqlServer\ServerEvents\\*instance_name*。 *instance_name*在默认安装中的默认为 MSSQLSERVER [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="permissions-and-server-authentication"></a>权限和服务器身份验证  
 若要访问 WMI Provider for Server Events，运行 WMI 管理应用程序的客户端必须对应于该应用程序的连接字符串中指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中已经过 Windows 身份验证的登录名或组。  
  
## <a name="permissions-and-event-notification-scope"></a>权限和事件通知作用域  
 WMI Provider for Server Events 将 WQL 查询转换为目标数据库中的事件通知。 正因为如此，调用应用程序不仅要具有访问提供程序所需的最低权限，在数据库中还要具有正确的权限来创建所需的事件通知。 以下是对这些权限的说明：  
  
-   若要创建以数据库为作用域的事件通知，至少需要在当前数据库中具有 CREATE DATABASE DDL EVENT NOTIFICATION 权限。  
  
-   若要对以服务器为作用域的 DDL 语句创建事件通知，至少需要在该服务器中具有 CREATE DDL EVENT NOTIFICATION 权限。  
  
-   若要对跟踪事件创建事件通知，至少需要在服务器中具有 CREATE TRACE EVENT NOTIFICATION 权限。  
  
-   若要创建以队列为作用域的事件通知，至少需要对该队列具有 ALTER 权限。  
  
 有关如何确定 WQL 查询的作用域的信息，请参阅 [将 WQL 与 WMI Provider for Server Events 结合使用](http://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx)。  
  
 为了对作用域进行说明，请考虑包含以下 WQL 查询的一个 WMI 提供程序应用程序：  
  
```  
SELECT * FROM ALTER_TABLE  
WHERE DatabaseName = "AdventureWorks2012"   
    AND SchemaName = "Person"  
    AND ObjectName = "Person"  
    AND ObjectType = "TABLE";  
```  
  
 该 WMI 提供程序将此查询转换为在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中创建的事件通知。 这意味着调用方必须具有创建这类事件通知所需的权限，具体而言，就是在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中具有 CREATE DATABASE DDL EVENT NOTIFICATION 权限。  
  
 如果 WQL 查询指定事件通知作用域为服务器级，例如通过发出查询 SELECT * FROM ALTER_TABLE，调用应用程序必须具有服务器级 CREATE DDL EVENT NOTIFICATION 权限。 请注意以服务器为作用域的事件通知存储在 master 数据库中。 你可以使用[sys.server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)目录视图以查看它们的元数据。  
  
> [!NOTE]  
>  WMI 提供程序创建的事件通知的作用域（服务器、数据库或对象）最终取决于 WMI 提供程序使用的权限验证过程的结果。 这受调用提供程序的用户的权限集和正在查询的数据库验证的影响。  
>   
>  在上面的示例中，提供程序首先尝试创建以数据库为作用域的事件通知 (`ON DATABASE`)。 如果提供程序验证数据库存在且调用方具有对其创建事件通知所需的权限，则注册成功。 如果失败，提供程序将尝试创建针对服务器的事件通知 (`ON SERVER`)。 假定此尝试成功，在此服务器上发生的所有 `ALTER_TABLE` 事件将从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程发送到 WMI 服务进程。 不过，提供程序筛选掉不适用于 `AdventureWorks` 数据库的所有事件。 尽管此过程可能增加事件作用域所需的网络流量，但是它使您在创建数据库前可以选择在数据库上注册 WQL 查询，然后在创建数据库并启动针对它的 DDL 活动后接收事件数据。  
  
## <a name="permissions-and-message-verification"></a>权限和消息验证  
 如果同时满足以下两个条件，则 WMI 提供程序不发送事件通知的消息：  
  
-   通过 WMI 提供程序创建了事件通知的用户已不存在于数据库中，或不再具有创建类似事件通知所需的权限。  
  
-   为以下事件创建事件通知：  
  
    -   DROP_LOGIN  
  
    -   ALTER_LOGIN  
  
    -   DROP_USER  
  
    -   ALTER_USER  
  
    -   ADD_ROLE_MEMBER  
  
    -   DROP_ROLE_MEMBER  
  
    -   ADD_SERVER_ROLE_MEMBER  
  
    -   DROP_SERVER_ROLE_MEMBER  
  
    -   DENY 或 REVOKE（仅适用于 ALTER DATABASE、ALTER ANY DATABASE EVENT NOTIFICATION、CREATE DATABASE DDL EVENT NOTIFICATION、CONTROL SERVER、ALTER ANY EVENT NOTIFICATION、CREATE DDL EVENT NOTIFICATION 或 CREATE TRACE EVENT NOTIFICATION 权限。）  
  
## <a name="working-with-event-data-on-the-client-side"></a>使用客户端的事件数据  
 在 WMI 提供程序后的服务器事件在目标数据库中，将创建所需的事件通知的事件通知事件将数据发送到名为的 msdb 中的目标服务**SQL/通知/ProcessWMIEventProviderNotification/v1.0**。 该目标服务将事件放入 **msdb** 中名为 **WMIEventProviderNotificationQueue**的队列。 （服务和队列都是提供程序首次连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时动态创建的。）提供程序然后读取此队列中的 XML 事件数据，在将其返回给客户端应用程序前将其转换为托管对象格式 (MOF)。 MOF 数据由 WQL 查询作为公共信息模型 (CIM) 类定义请求的事件属性组成。 每个属性具有相应的 CIM 类型。 例如，`SPID`作为 CIM 类型返回属性**Sint32**。 每个属性的 CIM 类型下列出每个事件类在[WMI Provider for Server Events 类和属性](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [WMI Provider for Server Events 的概念](http://technet.microsoft.com/library/ms180560.aspx)  
  
  
