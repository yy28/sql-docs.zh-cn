---
title: SQL Server 配置为接收远程表副本的并行数据仓库 |Microsoft Docs
description: 介绍如何配置外部 SMP SQL Server 实例以从并行数据仓库接收远程表副本。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ae6799d468d57dec04046b443c613823c0a8cb8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224688"
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies---parallel-data-warehouse"></a>配置外部 SMP SQL Server 以接收远程表副本的并行数据仓库
介绍如何配置外部的 SQL Server 实例，以从并行数据仓库接收远程表副本。  

本主题介绍配置远程表复制的配置步骤之一。 所有配置步骤的列表，请参阅[远程表复制](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>开始之前  
您可以配置外部的 SQL Server 之前，你必须：  
  
-   具有与 SQL Server 2008 Enterprise Edition 或更高版本准备好安装或已安装的 Windows 系统。 Windows 系统必须已配置根据中的说明[配置外部 Windows 系统为接收远程表副本使用 InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)。  
  
-   具有配置的 SQL Server 实例和 Windows 系统的功能的 Windows 管理员帐户。  
  
-   创建登录名并授予对目标数据库的权限的功能与 SQL Server 登录帐户 （如果尚未安装 SQL Server）。  
  
## <a name="HowToSQLServer"></a>配置外部 SMP SQL Server 以接收远程表副本  
远程表复制功能将从 SQL Server PDW 设备表复制到 Windows 系统运行的外部 SMP SQL Server 数据库。 配置外部的 Windows 系统，以接收远程表副本之后, 的下一步是安装和配置到 Windows 系统上的 SQL Server。  
  
若要配置 SQL Server，请使用以下步骤：  
  
1.  Windows 系统上安装 SQL Server 2008 Enterprise Edition 或更高版本。 这称为 SMP SQL Server。  
  
2.  SQL Server 配置为接受固定的 TCP 端口上的 TCP/IP 连接。 此配置默认处于禁用状态，并且必须启用以允许 SQL Server PDW 连接到 SMP SQL Server。  
  
3.  禁用 Windows 防火墙，或者配置 SMP SQL Server TCP 端口，以便它可用于启用 Windows 防火墙。  
  
4.  配置 SQL Server 以允许 SQL Server 身份验证模式。 并行数据始终导出使用 SQL Server 帐户进行身份验证。  
  
5.  确定将用于身份验证的 SMP SQL Server 上的 SQL Server 帐户。 该帐户授予创建、 删除，并将数据插入到目标数据库中的表的并行数据导出操作的权限。  
  
## <a name="BPSQLConfig"></a>远程表复制的 SMP SQL Server 配置最佳做法  
配置 SMP SQL Server 以接收远程表副本时，使用以下最佳做法以提高性能。  
  
1.  SQL Server 产品文档中所述，请遵循最佳做法。 例如，启用数据加密。 有关保护 SQL Server 的详细信息，请参阅[保护 SQL Server](../relational-databases/security/securing-sql-server.md) MSDN 上。  
  
2.  使用大容量日志模式或简单恢复模式。  
  
    在并行数据导出操作，数据是大容量插入到新创建的目标表。 为了在大容量插入期间的最大性能，目标数据库使用大容量日志或简单恢复模式设置。  
  
3.  使用 batch_size 选项以回收日志空间。  
  
    尽管大容量日志模式或简单恢复模型使用最小日志记录的大容量插入数据，但仍会发生某些日志记录。 若要防止日志文件增长得过大，请使用 SQL Server batch_size 选项以定期回收日志空间。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
