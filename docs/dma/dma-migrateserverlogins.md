---
title: 将 SQL Server 登录名迁移数据迁移助手 |Microsoft Docs
description: 了解如何迁移 SQL Server 登录名数据迁移助手
ms.custom: ''
ms.date: 10/22/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: 265ab37c47956400baa759b73838c7f2e66cc83e
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783264"
---
# <a name="migrate-sql-server-logins-with-data-migration-assistant"></a>将 SQL Server 登录名迁移数据迁移助手

本文概述如何使用数据迁移助手迁移 SQL Server 登录名。

> [!IMPORTANT]
> 本主题适用于涉及 SQL Server 升级到更高版本的本地产品或 Azure 虚拟机 SQL Server 的方案。

## <a name="which-logins-are-migrated"></a>迁移的登录名

- 你可以根据 Windows 主体（例如，域用户或 Windows 域组）迁移登录名。 还可以迁移基于 SQL 身份验证创建的登录名，也称为 SQL Server 登录名。

- 数据迁移助手当前不支持与独立安全证书（映射到证书的登录名）关联的登录名、独立的非对称密钥（映射到非对称密钥的登录名）以及映射到凭据的登录名。

- 数据迁移助手不会将**sa**登录名和服务器原理与用双引号（\#\#）括起来的名称一起使用，这些名称仅供内部使用。

- 默认情况下，数据迁移助手选择要迁移的所有合格登录名。 还可以选择要迁移的特定登录名。 当数据迁移助手迁移所有合格的登录名时，该登录用户的映射在迁移的数据库中保持不变。

  如果打算迁移特定的登录名，请确保在选择进行迁移的数据库中选择映射到一个或多个用户的登录名。

- 作为登录迁移的一部分，数据迁移助手还会移动用户定义的服务器角色，并将服务器级权限添加到用户定义的服务器角色。 角色的所有者将设置为**sa**主体。

## <a name="during-and-after-migration"></a>迁移期间和之后

- 作为登录迁移的一部分，数据迁移助手会将权限分配给目标 SQL Server 上的安全对象，因为它们存在于源 SQL Server 上。

  如果该登录名已存在于目标 SQL Server 上，数据迁移助手只迁移分配给安全对象的权限，而不会重新创建整个登录名。

- 如果目标服务器上已存在该登录名，数据迁移助手会尽力将登录名映射到数据库用户。

- 建议查看迁移结果，了解登录迁移的总体状态和任何建议的迁移后操作。

## <a name="resources"></a>Resources

[数据迁移助手（DMA）](../dma/dma-overview.md)

[数据迁移助手：配置设置](../dma/dma-configurationsettings.md)
