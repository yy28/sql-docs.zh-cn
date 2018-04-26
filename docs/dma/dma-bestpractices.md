---
title: 数据迁移助手 (SQL Server) 的最佳实践 |Microsoft 文档
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3b903d62a78b420ae6a267449b81919bd9db876e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="best-practices-for-running-data-migration-assistant"></a>用于运行数据迁移助手最佳实践
本文提供了有关安装、 评估和迁移下列的最佳做法信息。

## <a name="installation"></a>安装

不安装和直接在 SQL Server 宿主计算机上运行数据迁移助手。

## <a name="assessment"></a>评估

- 在非高峰时间运行的生产数据库上的评估。

- 执行**兼容性问题**和**新功能建议**评估，单独以减少评估持续时间。

## <a name="migration"></a>迁移

- 在非高峰时间迁移的服务器。

- 当迁移数据库，提供通过源服务器和目标服务器可访问的单个共享位置，并且如果可能，避免复制操作。 复制操作可能会造成延迟根据备份文件的大小。 复制操作也会增加一个额外步骤由于而导致失败的迁移的可能性。 当提供单个位置，则数据迁移助手会跳过复制操作。
 
    此外请确保以提供对共享文件夹的正确权限，为避免迁移失败。 该工具中指定了正确的权限。 如果在网络服务凭据下运行的 SQL Server 实例，向正确的权限在共享文件夹上的 SQL Server 实例的计算机帐户。

- 连接到源和目标服务器时，启用加密连接。 使用 SSL 加密会增加数据在数据迁移助手和 SQL Server 实例之间的网络上传输的安全性。 这是有益的尤其是在迁移 SQL 登录名。 如果不使用 SSL 加密，并且网络受到威胁的攻击者，正在迁移的 SQL 登录名了无法获取截获和/或修改上快速由攻击者。

    但是，如果所有访问都具有某项安全 Intranet 配置，则可能不需要使用加密。 启用加密时，就会减慢原因而导致的额外开销所需进行加密和解密数据包性能。 有关详细信息，请参阅[加密对 SQL Server 的连接](https://go.microsoft.com/fwlink/?linkid=832513)。
