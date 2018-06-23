---
title: 安全性概述（复制）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- authorization [SQL Server replication]
- cryptography [SQL Server replication]
- encryption [SQL Server replication]
- security [SQL Server replication], about security
- authentication [SQL Server replication]
ms.assetid: 27828fe4-3b54-4c33-886e-08e8279e34b5
caps.latest.revision: 44
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a3ca129d5dd03d788f639a51322ceb999a25e76a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016806"
---
# <a name="security-overview-replication"></a>安全性概述（复制）
  基本上，要保护复制环境的安全，您需要了解身份验证和授权选项，了解如何正确使用复制筛选功能以及了解保护复制环境的各个部分的具体措施。 复制环境包括分发服务器、发布服务器、订阅服务器和快照文件夹。 本章介绍复制安全性，但复制安全性是建立在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全性和 Windows 安全性基础上的。 因此应了解复制安全性的基础以及具体内容。 有关安全性的详细信息，请参阅 [Security Considerations for a SQL Server Installation](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)（安装 SQL Server 的安全注意事项）。 有关 Oracle 发布的安全注意事项的详细信息，请参阅主题 [Design Considerations and Limitations for Oracle Publishers](../non-sql/design-considerations-and-limitations-for-oracle-publishers.md)中的“复制安全模式”部分。  
  
## <a name="in-this-section"></a>本节内容  
 [威胁和漏洞缓解（复制）](threat-and-vulnerability-mitigation-replication.md)  
 讨论复制拓扑的潜在威胁，并介绍减少这些威胁的方法。  
  
 [标识和访问控制（复制）](identity-and-access-control-replication.md)  
 介绍如何使用身份验证、授权和筛选来帮助保护复制拓扑的安全。  
  
 [安全开发（复制）](secure-development-replication.md)  
 介绍复制安全行为、最佳复制安全配置和最低复制权限。  
  
 [安全部署（复制）](secure-deployment-replication.md)  
 介绍如何更好地保护复制拓扑的所有组件。  
  
## <a name="see-also"></a>请参阅  
 [安全性和保护（复制）](security-and-protection-replication.md)  
  
  