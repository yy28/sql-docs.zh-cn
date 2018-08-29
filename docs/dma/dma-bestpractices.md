---
title: 数据迁移助手 (SQL Server) 的最佳做法 |Microsoft Docs
description: 了解有关使用数据迁移助手将 SQL Server 数据库迁移最佳实践
ms.custom: ''
ms.date: 08/29/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 949576715472f5ad5ff99425635c9ad1d29a9823
ms.sourcegitcommit: fb269accc3786715c78f8b6e2ec38783a6eb63e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2018
ms.locfileid: "43152768"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>运行数据迁移助手的最佳做法
本文提供有关安装、 评估和迁移的一些最佳实践信息。

## <a name="installation"></a>安装
不要安装和直接在 SQL Server 主机上运行数据迁移助手。

## <a name="assessment"></a>评估
- 在非高峰时段，在生产数据库上运行评估。
- 执行**兼容性问题**并**新功能推荐**评估服务单独可减少评估持续时间。

## <a name="migration"></a>迁移
- 在非高峰时段迁移服务器。

- 时将数据库迁移，提供通过源服务器和目标服务器可访问的单个共享位置，并尽可能避免复制操作。 复制操作可能会造成延迟根据备份文件的大小。 复制操作也会增加迁移将由于一个额外步骤会失败的可能性。 当提供单个位置，则数据迁移助手会跳过复制操作。
 
    此外，请确保提供正确的权限的共享文件夹为避免迁移失败。 在工具中指定正确的权限。 如果在网络服务凭据下运行的 SQL Server 实例，向正确的权限在共享文件夹上的 SQL Server 实例的计算机帐户。

- 连接到源和目标服务器时，启用加密连接。 使用 SSL 加密将增强通过数据迁移助手和 SQL Server 实例，是有益的尤其是在迁移 SQL 登录名之间的网络传输的数据的安全性。 如果不使用 SSL 加密网络攻击的攻击者，要迁移的 SQL 登录名了可能能够截取和/或修改在实时的攻击者。

    但是，如果所有访问都具有某项安全 Intranet 配置，则可能不需要使用加密。 启用加密会降低性能，因为这是进行加密和解密数据包所需的额外系统开销。 有关详细信息，请参阅[加密与 SQL Server 的连接](https://go.microsoft.com/fwlink/?linkid=832513)。
