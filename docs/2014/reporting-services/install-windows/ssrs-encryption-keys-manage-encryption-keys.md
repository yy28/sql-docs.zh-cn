---
title: 配置和管理加密密钥（SSRS 配置管理器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- encryption keys [Reporting Services]
- private keys [Reporting Services]
- cryptography [Reporting Services]
- symmetric keys [Reporting Services]
- encryption [Reporting Services]
- public keys [Reporting Services]
ms.assetid: 58e61636-88a2-4338-ae5f-3dd210aee887
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4858b9844c4b07d270c615d30089d104bb7ba76a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108724"
---
# <a name="configure-and-manage-encryption-keys-ssrs-configuration-manager"></a>配置和管理加密密钥（SSRS 配置管理器）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用加密密钥来保护存储在报表服务器数据库中的凭据和连接信息。 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，通过一组用于保护敏感数据的公钥、私钥和对称密钥支持加密。 安装或配置报表服务器时，在报表服务器初始化期间会创建对称密钥，报表服务器使用此对称密钥对存储在报表服务器中的敏感数据进行加密。 公钥和私钥由操作系统创建，用于保护对称密钥。 对于在报表服务器数据库中存储敏感数据的每个报表服务器实例，都要创建一个公钥私钥对。  
  
 管理加密密钥包括创建对称密钥的备份副本以及了解密钥的还原、删除或更改的时间和方式。 如果迁移报表服务器安装或配置扩展部署，则必须拥有对称密钥的备份副本，以便可以将其应用于新的安装。  
  
> [!IMPORTANT]  
>  定期更改 Reporting Services 加密密钥是确保安全的好办法。 建议在升级 Reporting Services 主版本后立即更改密钥。 升级后更改密钥将使在升级周期外更改 Reporting Services 加密密钥所导致的额外服务中断降到最低程度。  
  
 若要管理对称密钥，可以使用 Reporting Services 配置工具或 **rskeymgmt** 实用工具。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中包括的工具仅用于管理对称密钥（公钥和私钥由操作系统管理）。 Reporting Services 配置工具和 **rskeymgmt** 实用工具都支持以下任务：  
  
-   备份对称密钥的副本，以便可以使用该副本来恢复报表服务器安装或作为计划迁移的一部分。  
  
-   将以前保存的对称密钥还原到报表服务器数据库，以允许新的报表服务器实例访问最初不是由其进行加密的现有数据。  
  
-   在无法再访问加密数据时删除报表服务器数据库中的加密数据，这种情况极少出现。  
  
-   当对称密钥遭到破坏时重新创建对称密钥并重新加密数据，这种情况极少出现。 作为安全性方面的最佳做法，您应定期（例如，每隔几个月）重新创建对称密钥，以保护报表服务器数据库，使其能够抵御试图解开密钥的网络攻击。  
  
-   在报表服务器扩展部署（多个报表服务器同时共享一个报表服务器数据库以及为该数据库提供可逆加密的对称密钥）中添加或删除报表服务器实例。  
  
## <a name="in-this-section"></a>本节内容  
 [初始化 Report Server（SSRS 配置管理器）](ssrs-encryption-keys-initialize-a-report-server.md)  
 介绍如何创建加密密钥。  
  
 [备份和还原 Reporting Services 加密密钥](ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
 介绍如何备份加密密钥以及如何还原备份以恢复或迁移报表服务器安装。  
  
 [存储加密的 Report Server 数据（SSRS 配置管理器）](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
 介绍报表服务器的加密。  
  
 [删除和重新创建加密密钥（SSRS 配置管理器）](ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)  
 介绍如何用新版本替换对称密钥以及在无法验证对称密钥时如何重新开始。  
  
 [添加和删除扩展部署的加密密钥（SSRS 配置管理器）](add-and-remove-encryption-keys-for-scale-out-deployment.md)  
 介绍如何添加和删除加密密钥以控制在扩展部署中包括哪些报表服务器。  
  
## <a name="see-also"></a>请参阅  
 [存储加密的 Report Server 数据（SSRS 配置管理器）](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
