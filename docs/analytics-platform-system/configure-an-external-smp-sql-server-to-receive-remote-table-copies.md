---
title: "外部 SMP SQL Server 配置为接收远程表副本 (PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bbd2ed6-064e-4b45-b67b-608dc0f2b2bc
caps.latest.revision: "13"
ms.openlocfilehash: 18b61d60e8ca771feab84b24a9ff53cc7bdfc193
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies"></a>配置外部 SMP SQL 服务器以接收远程表副本
描述如何配置一个外部的 SQL Server 实例，以便从 SQL Server PDW 接收远程表副本。  
  
本主题介绍配置远程表复制的配置步骤之一。 有关所有配置步骤的列表，请参阅[远程表复制](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>开始之前  
你可以配置外部的 SQL Server 之前，你必须：  
  
-   具有 Windows 系统与 SQL Server 2008 Enterprise Edition 或更高版本准备好安装或已安装。 Windows 系统必须已配置中的说明根据[配置外部 Windows 系统为接收远程表副本使用 InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)。  
  
-   能够将 SQL Server 实例和 Windows 系统配置 Windows 管理员帐户。  
  
-   SQL Server 登录帐户 （如果已安装 SQL Server） 能够创建登录名并授予对目标数据库的权限。  
  
## <a name="HowToSQLServer"></a>配置外部 SMP SQL 服务器以接收远程表副本  
远程表复制功能将从 SQL Server PDW 装置表复制到 Windows 系统正在运行的外部 SMP SQL Server 数据库中。 在配置外部的 Windows 系统，以接收远程表副本后下, 一步是安装和配置到 Windows 系统上的 SQL Server。  
  
若要配置 SQL Server，请使用以下步骤：  
  
1.  在 Windows 系统上安装 SQL Server 2008 Enterprise Edition 或更高版本。 这被称为 SMP SQL Server。  
  
2.  配置 SQL Server 以接受固定的 TCP 端口上的 TCP/IP 连接。 此配置默认处于禁用状态，必须启用才能允许 SQL Server PDW 以连接到 SMP SQL Server。  
  
3.  禁用 Windows 防火墙，或者配置 SMP SQL Server TCP 端口，以便将启用 Windows 防火墙工作。  
  
4.  配置 SQL Server 以允许 SQL Server 身份验证模式。 并行数据始终导出使用 SQL Server 帐户进行身份验证。  
  
5.  确定将用于身份验证的 SMP SQL 服务器上的 SQL Server 帐户。 该帐户授予权限创建、 删除，并将数据插入到并行数据导出操作的目标数据库中的表。  
  
## <a name="BPSQLConfig"></a>SMP SQL Server 配置为远程表副本的最佳实践  
配置 SMP SQL Server，以接收远程表副本时，使用下列最佳方案来提高性能。  
  
1.  SQL Server 产品文档中所述，请遵循最佳做法。 例如，启用数据加密。 有关保护 SQL Server 的详细信息，请参阅[保护 SQL Server](../relational-databases/security/securing-sql-server.md) MSDN 上。  
  
2.  使用大容量日志或简单恢复模式。  
  
    在并行数据导出操作，数据是大容量插入到新创建的目标表。 在大容量插入期间的最大性能，将设置目标数据库以使用大容量日志或简单恢复模式。  
  
3.  使用 batch_size 选项来回收日志空间。  
  
    尽管大容量日志或简单恢复模型使用最小日志记录的大容量插入数据，但仍出现某些日志记录。 若要防止日志文件增长过大，请使用 SQL Server batch_size 选项来定期回收日志空间。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
