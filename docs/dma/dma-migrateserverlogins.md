---
title: 迁移 SQL Server 登录名 （数据迁移助手） |Microsoft 文档
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 23da8fe364ffad914013719f54871e85213befc5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-sql-server-logins-using-data-migration-assistant"></a>迁移 SQL Server 登录名使用数据迁移助手

本文概述了使用数据迁移助手的迁移 SQL Server 登录名。 

## <a name="key-concepts"></a>关键概念
以下是关键的概念。

- 你可以迁移基于 Windows 主体 （如域用户或 Windows 域组） 的登录名。 您也可以将迁移基于 SQL 身份验证，也称为 SQL Server 登录名创建的登录名。

- 数据迁移助手目前不支持关联一个独立的安全证书 （登录名映射到证书）、 独立的非对称密钥 （映射到非对称密钥登录名） 映射到凭据的登录名的登录名。

- 数据迁移助手不会移动**sa**名称由双井号括起来的登录名和服务器原则 (\#\#)，这是仅供内部使用。

- 默认情况下，数据迁移 Assistatn 选择所有限定登录名迁移。 或者，您可以选择要迁移的特定登录名。 当数据迁移助手迁移所有限定登录名时，登录用户映射中保持不变的迁移的数据库。 

  如果你打算迁移特定的登录名，请确保选择映射到选择要迁移的数据库中的一个或多个用户的登录名。

- 作为登录名迁移的一部分，数据迁移助手还移动用户定义的服务器角色并将服务器级权限添加到用户定义的服务器角色。 角色的所有者将设置为**sa**主体。

- 作为登录名迁移的一部分，数据迁移助手将权限分配到目标 SQL Server 上的安全对象因为它们在源 SQL Server 上存在。 

  如果在目标 SQL Server 上已存在登录名，数据迁移助手会迁移仅分配给安全对象的权限，而且不会重新创建整个登录名。

- 数据迁移助手尽最大努力中，若要将登录名映射到数据库用户，如果目标服务器上已存在登录名。

- 建议你查看要了解的登录名迁移和任何建议的迁移后操作的总体状态的迁移结果。

## <a name="resources"></a>Resources

[数据迁移助手 (DMA)](../dma/dma-overview.md)

[数据迁移助手： 配置设置](../dma/dma-configurationsettings.md)
