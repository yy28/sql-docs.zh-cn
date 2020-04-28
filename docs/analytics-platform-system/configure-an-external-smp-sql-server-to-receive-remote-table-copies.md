---
title: 配置 SQL Server 以接收远程表副本
description: 描述如何将外部 SMP SQL Server 实例配置为从并行数据仓库接收远程表副本。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3e5475e86582ede2e6fa7ca5a302bba7ee74faa3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401318"
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies---parallel-data-warehouse"></a>配置外部 SMP SQL Server 以接收远程表副本-并行数据仓库
描述如何将外部 SQL Server 实例配置为从并行数据仓库接收远程表副本。  

本主题介绍配置远程表复制的配置步骤之一。 有关所有配置步骤的列表，请参阅[远程表复制](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>开始之前  
必须先执行以下操作，然后才能配置外部 SQL Server：  
  
-   有一个 Windows 系统，其中包含 SQL Server 2008 企业版或更高版本，可以安装或已经安装。 Windows 系统必须已根据[配置外部 Windows 系统中的说明配置，以使用不受使用的来接收远程表副本](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)。  
  
-   能够配置 SQL Server 实例和 Windows 系统的 Windows 管理员帐户。  
  
-   SQL Server 的登录帐户（如果已安装 SQL Server），并且能够创建登录名并授予对目标数据库的权限。  
  
## <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies"></a><a name="HowToSQLServer"></a>配置外部 SMP SQL Server 以接收远程表副本  
"远程表复制" 功能将表从 SQL Server PDW 设备复制到在 Windows 系统上运行的外部 SMP SQL Server 数据库。 在将外部 Windows 系统配置为接收远程表副本后，下一步是在 Windows 系统上安装和配置 SQL Server。  
  
若要配置 SQL Server，请使用以下步骤：  
  
1.  在 Windows 系统上安装 SQL Server 2008 Enterprise Edition 或更高版本。 这称为 SMP SQL Server。  
  
2.  配置 SQL Server 以接受固定 TCP 端口上的 TCP/IP 连接。 此配置在默认情况下处于禁用状态，并且必须启用以允许 SQL Server PDW 连接到 SMP SQL Server。  
  
3.  禁用 Windows 防火墙或配置 SMP SQL Server TCP 端口，使其可用于启用 Windows 防火墙。  
  
4.  将 SQL Server 配置为允许 SQL Server 身份验证模式。 并行数据导出始终使用 SQL Server 帐户进行身份验证。  
  
5.  确定将用于身份验证的 SMP SQL Server 上的 SQL Server 帐户。 为并行数据导出操作授予该帐户在目标数据库的表中创建、删除和插入数据的权限。  
  
## <a name="best-practices-for-smp-sql-server-configuration-for-remote-table-copy"></a><a name="BPSQLConfig"></a>远程表复制的 SMP SQL Server 配置的最佳实践  
配置 SMP SQL Server 以接收远程表副本时，请使用以下最佳做法来提高性能。  
  
1.  按照 SQL Server 产品文档中所述的最佳实践进行操作。 例如，启用数据加密。 有关保护 SQL Server 的详细信息，请参阅 MSDN 上的[保护 SQL Server](../relational-databases/security/securing-sql-server.md) 。  
  
2.  使用大容量日志恢复模式或简单恢复模式。  
  
    在并行数据导出操作期间，会将数据大容量插入到新创建的目标表中。 为了在大容量插入期间获得最大性能，请将目标数据库设置为使用大容量日志模式或简单恢复模式。  
  
3.  使用 batch_size 选项可以回收日志空间。  
  
    虽然大容量日志恢复模式或简单恢复模式对大容量插入的数据使用最小日志记录，但仍会出现一些日志记录。 若要防止日志文件增长太大，请使用 SQL Server batch_size 选项定期回收日志空间。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
