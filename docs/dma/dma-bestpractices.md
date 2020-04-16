---
title: 数据迁移助手的最佳做法
description: 使用数据迁移助手了解迁移 SQL Server 数据库的最佳做法
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: f2bfbb79a8a4803bb56e3dce85f575e8cf257b4a
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388155"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>运行数据迁移助手的最佳做法
本文提供了一些用于安装、评估和迁移的最佳做法信息。

## <a name="installation"></a>安装
不要在 SQL Server 主机上直接安装和运行数据迁移助手。

## <a name="assessment"></a>评估
- 在非高峰时间对生产数据库运行评估。
- 分别执行**兼容性问题和****新功能建议**评估，以减少评估持续时间。

## <a name="migration"></a>迁移
- 在非高峰时间迁移服务器。

- 迁移数据库时，提供源服务器和目标服务器可访问的单个共享位置，并尽可能避免复制操作。 复制操作可能会根据备份文件的大小引入延迟。 复制操作还会增加迁移由于额外步骤而失败的可能性。 当提供单个位置时，数据迁移助手会绕过复制操作。
 
    此外，请确保向共享文件夹提供正确的权限，以避免迁移失败。 该工具中指定了正确的权限。 如果 SQL Server 实例在网络服务凭据下运行，则将共享文件夹的正确权限授予 SQL Server 实例的计算机帐户。

- 连接到源服务器和目标服务器时启用加密连接。 使用 TLS 加密可提高数据迁移助手和 SQL Server 实例之间通过网络传输的数据的安全性，这在迁移 SQL 登录时尤其有益。 如果未使用 TLS 加密，并且网络受到攻击者的威胁，则正在迁移的 SQL 登录可能会被攻击者实时拦截和/或修改。

    但是，如果所有访问都具有某项安全 Intranet 配置，则可能不需要使用加密。 启用加密会降低性能，因为加密和解密数据包需要额外的开销。 有关详细信息，请参阅 [加密到 SQL 服务器的连接](https://go.microsoft.com/fwlink/?linkid=832513)。
    
- 在迁移数据之前，请检查源数据库和目标数据库上的不受信任的约束。 迁移后，请再次分析目标数据库，以查看作为数据移动的一部分，是否有任何约束变得不受信任的约束。 根据需要修复不受信任的约束。 使约束不受信任可能会导致执行计划不佳，并且可能会影响性能。
