---
title: 合并复制 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], about merge replication
- merge replication [SQL Server replication]
ms.assetid: ff87c368-4c00-4e48-809d-ea752839551e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8617fcbc7204dfe29d3f6a02a0240812b5bd682c
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175816"
---
# <a name="merge-replication"></a>合并复制
  与事务复制相同，合并复制通常也是从发布数据库对象和数据的快照开始， 并且用触发器跟踪在发布服务器和订阅服务器上所做的后续数据更改和架构修改。 订阅服务器在连接到网络时将与发布服务器进行同步，并交换自上次同步以来发布服务器和订阅服务器之间发生更改的所有行。

 合并复制通常用于服务器到客户端的环境中。 合并复制适用于下列各种情况：

-   多个订阅服务器可能会在不同时间更新同一数据，并将其更改传播到发布服务器和其他订阅服务器。

-   订阅服务器需要接收数据，脱机更改数据，并在以后与发布服务器和其他订阅服务器同步更改。

-   每个订阅服务器都需要不同的数据分区。

-   可能会发生冲突，并且在冲突发生时，您需要具有检测和解决冲突的能力。

-   应用程序需要最终的数据更改结果，而不是访问中间数据状态。 例如，如果在订阅服务器与发布服务器进行同步之前，订阅服务器上的行更改了五次，则该行在发布服务器上仅更改一次来反映最终数据更改（也就是第五次更改的值）。

 合并复制允许不同站点自主工作，并在以后将更新合并成一个统一的结果。 由于更新是在多个节点上进行的，同一数据可能由发布服务器和多个订阅服务器进行了更新。 因此，在合并更新时可能会产生冲突，合并复制提供了多种处理冲突的方法。

 合并复制是由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 快照代理和合并代理实现的。 如果发布未经筛选或使用静态筛选器，快照代理将创建单个快照。 如果发布使用参数化筛选器，则快照代理将为每个数据分区创建一个快照。 合并代理将初始快照应用于订阅服务器。 它还将合并自初始快照创建后发布服务器或订阅服务器上所发生的增量数据更改，并根据所配置的规则检测和解决任何冲突。

 若要跟踪更改，合并复制（和带有排队更新订阅的事务复制）必须能够唯一地标识每个已发布表中的每一行。 为了完成这一合并复制，需要向每个表添加列 `rowguid`，除非表中已包含一个数据类型为 `uniqueidentifier` 且设置了 `ROWGUIDCOL` 属性的列（这种情况下将使用此列）。 如果从发布中删除表，则删除 `rowguid` 列；如果将现有列用于跟踪，则不删除该列。 筛选器不能包含复制所用的 `rowguidcol` 来标识行。 提供 `newid()` 函数，为 `rowguid` 列提供默认值，但用户可以按需为每行提供 GUID。 不过，请不要提供值 00000000-0000-0000-0000-000000000000。

 下面的关系图显示了合并复制中使用的组件。

 ![合并复制组件和数据流](../media/merge.gif "合并复制组件和数据流")


