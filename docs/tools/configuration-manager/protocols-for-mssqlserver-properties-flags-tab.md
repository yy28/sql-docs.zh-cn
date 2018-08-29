---
title: MSSQLSERVER 属性的协议（“标志”选项卡）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQLSERVER property protocols
ms.assetid: 4d38e6e9-f95f-4e79-ae45-89f631037528
caps.latest.revision: 32
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 07d84ac33833259d28f7ecf01487089b8105b5a5
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "42785928"
---
# <a name="protocols-for-mssqlserver-properties-flags-tab"></a>MSSQLSERVER 的协议属性（“标志”选项卡）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  当服务器上装有证书时，使用 **“MSSQLSERVER 的协议属性”** 对话框中的 **“标志”** 选项卡可以查看或指定协议加密以及隐藏实例选项。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 设置，必须重新启动 **ForceEncryption** 。  
  
 若要加密连接，应为 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 提供一个证书。 如果未安装证书，则实例启动后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将生成一个自签名证书。 此自签名证书可代替可信证书颁发机构颁发的证书，但它不提供身份验证，也不具有不可否认性。  
  
> [!CAUTION]  
>  使用自签名证书加密的安全套接字层 (SSL) 连接不提供强安全性。 它们容易在传输中途受到攻击。 在生产环境中或在连接到 Internet 的服务器上，不应依赖使用自签名证书的 SSL。  
  
 有关加密的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书中的“加密与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接”。  
  
 登录过程始终是加密的。 如果将 **ForceEncryption** 设为 **“是”**，则将对所有客户端/服务器通信进行加密，并必须将连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的客户端配置为信任服务器证书的根颁发机构。 有关详细信息，请参阅 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 联机丛书中的“如何启用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的加密连接（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器）”。  
  
## <a name="cluster-servers"></a>集群服务器  
 若要在故障转移群集中使用加密，必须在故障转移群集中的所有节点上安装具有完全限定的虚拟服务器 DNS 名称的服务器证书。 例如，如果有一个包含两个分别名为“test1.\<your company>.com”和“test2.\<your company>.com”节点的群集，还有一个名为“virtsql”的虚拟服务器，则需要在这两个节点上安装“virtsql.\<your company>.com”的证书。 然后，可以选中 **SQL Server 配置管理器** 中的 **ForceEncryption** 复选框以将故障转移群集配置为使用加密。  
  
## <a name="options"></a>选项  
 **ForceEncryption**  
 强制协议加密。 加密是通过将数据更改为不可读的形式来保密敏感信息的方法。 即使在传输过程中有人查看了传输数据包，加密也可以确保数据安全。 若要使用渠道绑定，请将 **“强行加密”** 设置为 **“打开”** ，并在 **“高级”** 选项卡上配置 **“扩展保护”** 。  
  
 **HideInstance**  
 防止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务向尝试通过使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] “浏览” **按钮来查找实例的客户端计算机公开此** 实例。 在服务器上存在命名实例的情况下，若要连接，则客户端应用程序必须指定协议端点信息。 例如，端口号或命名管道名（如 **tcp:server,5000**）。 有关详细信息，请参阅 [Logging In to SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md)。  
  
 有关详细信息，请参阅联机丛书中的“如何启用数据库引擎的加密连接（SQL Server 配置管理器）”。  
  
  
