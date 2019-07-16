---
title: 包含文件
description: 包含文件
services: sql-database
author: MightyPen
ms.service: sql-database
ms.topic: include
ms.date: 04/05/2018
ms.author: genemi
ms.custom: include file
ms.openlocfilehash: 0e7d549c2f3b02349007815019cc47647f172f73
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68213537"
---
## <a name="specifying-application-intent"></a>指定应用程序意向

关键字**ApplicationIntent**可以在连接字符串中指定。 可分配的值为**ReadWrite**或**ReadOnly**。 默认值是**ReadWrite**。

当**ApplicationIntent = ReadOnly**，客户端连接时将请求读取工作负荷。 在连接时和在期间，服务器强制执行该意向**使用**数据库语句。

 ApplicationIntent 关键字不适用于早期的只读数据库。  


#### <a name="targets-of-readonly"></a>ReadOnly 的目标

当连接选择**ReadOnly**，连接分配到任何数据库可能存在的特殊配置如下：

- [Always On](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - 数据库可允许或禁止目标 Always On 数据库上的读取工作负载。 选择此选项通过使用控制**ALLOW_CONNECTIONS**子句**PRIMARY_ROLE**并**SECONDARY_ROLE** TRANSACT-SQL 语句。

- [异地复制](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)

- [读取横向扩展](https://docs.microsoft.com/azure/sql-database/sql-database-read-scale-out)

如果这些特殊的目标都不可用，则从读取常规数据库。

&nbsp;

**ApplicationIntent**关键词*只读路由*。


## <a name="read-only-routing"></a>只读路由

只读路由是一项功能，可用于确保数据库的只读副本的可用性。 若要启用只读路由，所有以下应用：

- 您必须连接到某一 AlwaysOn 可用性组侦听器。

- **ApplicationIntent** 连接字符串关键字必须设置为 **ReadOnly**。

- 数据库管理员必须配置该可用性组以便启用只读路由。

多个连接使用只读路由不是所有可能会连接到同一只读副本。 对数据库同步进行更改或对服务器的路由配置进行更改可能导致客户端连接到不同的只读副本。 您可以确保所有只读请求连接到相同的只读副本。 确保通过此一致性*不*传递到某一可用性组侦听器**Server**连接字符串关键字。 而是指定只读实例的名称。

只读路由可能会长于连接到主副本。 等待时间较长是因为只读路由首先会连接到主副本，然后查找最合适的可读辅助副本。 由于这些多个 staps，应增加到至少 30 秒后你登录超时值。

