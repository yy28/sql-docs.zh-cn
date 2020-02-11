---
title: 数据迁移助手的最佳做法
description: 了解通过数据迁移助手迁移 SQL Server 数据库的最佳做法
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
ms.openlocfilehash: e0f81a49af551836881ca71b49ff6a15d22a9897
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "76162618"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>运行数据迁移助手的最佳做法
本文提供了有关安装、评估和迁移的一些最佳实践信息。

## <a name="installation"></a>安装
请勿直接在 SQL Server 主机计算机上安装并运行数据迁移助手。

## <a name="assessment"></a>评估
- 在非高峰时间对生产数据库运行评估。
- 单独执行**兼容性问题**和**新功能建议**评估，以减少评估持续时间。

## <a name="migration"></a>迁移
- 在非高峰时间迁移服务器。

- 迁移数据库时，请提供源服务器和目标服务器可以访问的单个共享位置，并尽可能避免复制操作。 复制操作可能会根据备份文件的大小引入延迟。 复制操作还增加了由于额外步骤导致迁移失败的几率。 提供单个位置时，数据迁移助手绕过复制操作。
 
    此外，请确保为共享文件夹提供正确的权限，以避免迁移失败。 在该工具中指定了正确的权限。 如果 SQL Server 实例使用 "网络服务凭据" 运行，请向 SQL Server 实例的计算机帐户授予对共享文件夹的正确权限。

- 连接到源服务器和目标服务器时，启用加密连接。 使用 SSL 加密会提高在数据迁移助手和 SQL Server 实例之间跨网络传输的数据的安全性，这在迁移 SQL 登录名时尤为有用。 如果未使用 SSL 加密并且网络遭到攻击者的攻击，则迁移的 SQL 登录名可能会由攻击者动态截获和/或修改。

    但是，如果所有访问都具有某项安全 Intranet 配置，则可能不需要使用加密。 启用加密会降低性能，因为加密和解密数据包需要额外的开销。 有关详细信息，请参阅 [加密连接 SQL Server](https://go.microsoft.com/fwlink/?linkid=832513)。
    
- 在迁移数据之前，检查源数据库和目标数据库上的不受信任的约束。 迁移后，请再次分析目标数据库，以确定是否有任何约束在数据移动过程中不受信任。 根据需要修复不受信任的约束。 使约束不受信任可能会导致执行计划不佳，并且可能会影响性能。
