---
title: SQL Server Native Client 配置属性（“标志”选项卡）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bf95081d3c4657dd147e06ae54d413dd96c4c18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63028287"
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>SQL Server Native Client 配置属性（“标志”选项卡）
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]此计算机上的客户端使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 库文件中提供的协议与服务器进行通信。 使用本页可将客户端计算机配置为使用安全套接字层 (SSL) 请求加密的连接。 如果无法建立加密的连接，则连接将失败。  
  
 登录过程始终是加密的。 以下选项仅适用于加密数据。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何加密通信的详细信息，以及如何将客户端配置为信任服务器证书的根颁发机构的说明，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书中的“加密与 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的连接”和“如何启用与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的加密连接（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器）”。  
  
## <a name="options"></a>选项  
 **强制协议加密**  
 使用 SSL 请求连接。  
  
 **信任服务器证书**  
 当设置为****“否”时，客户端进程将尝试验证服务器证书。 客户端和服务器均必须拥有公共证书颁发机构颁发的证书。 如果客户端计算机上没有证书，或如果验证证书失败，则连接将终止。  
  
 当设置为****“是”时，客户端不会验证服务器证书，而是使用自签名证书。  
  
 只有在 "**强制协议加密**" 设置为 **"是"** 时，才可使用 "**信任服务器证书**"。  
  
  
