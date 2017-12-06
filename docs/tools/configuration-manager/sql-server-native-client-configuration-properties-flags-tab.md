---
title: "SQL Server Native Client 配置属性 （标志选项卡） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 96cb3184afd9481f91ef9d08ad4ae112425cbaac
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>SQL Server Native Client 配置属性（“标志”选项卡）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]此计算机上的客户端与通信[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务器使用中提供的协议[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 库文件。 使用本页可将客户端计算机配置为使用安全套接字层 (SSL) 请求加密的连接。 如果无法建立加密的连接，则连接将失败。  
  
 登录过程始终是加密的。 以下选项仅适用于加密数据。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何加密通信的详细信息，以及如何将客户端配置为信任服务器证书的根颁发机构的说明，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书中的“加密与 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的连接”和“如何启用与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的加密连接（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器）”。  
  
## <a name="options"></a>选项  
 **强制协议加密**  
 使用 SSL 请求连接。  
  
 **信任服务器证书**  
 当设置为“否”时，客户端进程将尝试验证服务器证书。 客户端和服务器均必须拥有公共证书颁发机构颁发的证书。 如果客户端计算机上没有证书，或如果验证证书失败，则连接将终止。  
  
 当设置为“是”时，客户端不会验证服务器证书，而是使用自签名证书。  
  
 仅在“强制协议加密” 设置为“是”  时，才可使用“信任服务器证书” 。  
  
  
