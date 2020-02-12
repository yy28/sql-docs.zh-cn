---
title: include 文件
description: include 文件
services: sql-database
author: MightyPen
ms.service: sql-database
ms.topic: include
ms.date: 04/05/2018
ms.author: genemi
ms.custom: include file
ms.openlocfilehash: 0e7d549c2f3b02349007815019cc47647f172f73
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68213537"
---
## <a name="specifying-application-intent"></a>指定应用程序意向

可以在连接字符串中指定关键字 ApplicationIntent  。 可赋值为 ReadWrite  或 ReadOnly  。 默认值为 ReadWrite  。

若为 ApplicationIntent=ReadOnly  ，客户端在连接时请求读取工作负荷。 服务器在连接时和在执行 USE  数据库语句期间强制执行此意向。

 ApplicationIntent 关键字不适用于早期的只读数据库。  


#### <a name="targets-of-readonly"></a>ReadOnly 的目标

如果连接选择 ReadOnly  ，连接就会分配到数据库可能存在的下列任何特殊配置：

- [Always On](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - 数据库可允许或禁止目标 Always On 数据库上的读取工作负载。 此选择是通过使用 PRIMARY_ROLE  和 SECONDARY_ROLE  Transact-SQL 语句的 ALLOW_CONNECTIONS  子句来控制的。

- [异地复制](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)

- [读取横向扩展](https://docs.microsoft.com/azure/sql-database/sql-database-read-scale-out)

如果这些特殊目标都不可用，则从常规数据库读取。

&nbsp;

ApplicationIntent  关键字可启用只读路由  。


## <a name="read-only-routing"></a>只读路由

只读路由是一项功能，可用于确保数据库的只读副本的可用性。 若要启用只读路由，必须遵守以下所有要求：

- 您必须连接到某一 AlwaysOn 可用性组侦听器。

- **ApplicationIntent** 连接字符串关键字必须设置为 **ReadOnly**。

- 数据库管理员必须配置该可用性组以便启用只读路由。

使用只读路由的多个连接可能不会全部连接到相同的只读副本。 对数据库同步进行更改或对服务器的路由配置进行更改可能导致客户端连接到不同的只读副本。 可以确保所有只读请求都连接到相同的只读副本。 通过不  向 Server  连接字符串关键字传递可用性组侦听程序，确保连接到相同的只读副本。 而是指定只读实例的名称。

只读路由可能比连接到主路由需要更长的时间。 等待时间较长是因为只读路由首先会连接到主副本，然后查找最合适的可读辅助副本。 由于使用了多个阻止，应将登录超时提高到至少 30 秒。

