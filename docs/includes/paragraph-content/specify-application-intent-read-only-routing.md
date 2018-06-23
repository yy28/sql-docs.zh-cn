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
ms.openlocfilehash: 842a7377bcd6bdcb649a78b2f31eb66de95bc5a3
ms.sourcegitcommit: a98ed7872afc055c65aa9697d571f8b300f6eeb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313393"
---
## <a name="specifying-application-intent"></a>指定应用程序意向

关键字**ApplicationIntent**可以在你的连接字符串中指定。 可赋值的值是**ReadWrite**或**ReadOnly**。 默认值是**ReadWrite**。

当**ApplicationIntent = ReadOnly**，客户端连接时请求读工作负荷。 在连接时和期间，服务器强制执行该意向**使用**数据库语句。

**ApplicationIntent**关键字不适用于旧的只读数据库。  


#### <a name="targets-of-readonly"></a>为 ReadOnly 的目标

当连接选择**ReadOnly**，连接分配到任何可能存在的数据库的以下特殊配置：

- [Alwayson](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - 数据库可以允许或禁止目标 Alwayson 数据库上的读取工作负荷。 选择此选项通过使用控制**ALLOW_CONNECTIONS**子句**PRIMARY_ROLE**和**SECONDARY_ROLE** TRANSACT-SQL 语句。

- [异地复制](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)

- [读取扩展](https://docs.microsoft.com/azure/sql-database/sql-database-read-scale-out)

如果任何这些特殊的目标都不可用，将从读取常规数据库。

&nbsp;

**ApplicationIntent**关键字允许*只读路由*。


## <a name="read-only-routing"></a>只读路由

只读路由是一项功能，可用于确保数据库的只读副本的可用性。 若要启用只读路由，所有以下应用：

- 您必须连接到某一 AlwaysOn 可用性组侦听器。

- **ApplicationIntent** 连接字符串关键字必须设置为 **ReadOnly**。

- 数据库管理员必须配置该可用性组以便启用只读路由。

多个连接使用只读路由可能会不是所有连接到相同的只读副本。 对数据库同步进行更改或对服务器的路由配置进行更改可能导致客户端连接到不同的只读副本。 你可以确保所有只读请求连接到相同的只读副本。 确保通过此一致性*不*传递到一个可用性组侦听器**服务器**连接字符串关键字。 而是指定只读实例的名称。

只读路由可能需要超过连接到主副本。 长等待是因为只读路由首先连接到主副本，并随后查找最佳可读的辅助数据库。 由于这些多个 staps，则应增加到你登录超时值为至少 30 秒。

