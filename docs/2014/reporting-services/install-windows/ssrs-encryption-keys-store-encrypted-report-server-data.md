---
title: 存储加密的报表服务器数据（SSRS 配置管理器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], encryption
- credentials [Reporting Services]
- cryptography [Reporting Services]
- confidential reports [Reporting Services]
- encryption [Reporting Services]
- databases [Reporting Services], encryption
ms.assetid: ac0f4d4d-fc4b-4c62-a693-b86e712e75f2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8156e3d62e8aac027499ad1e267e1f6e14f5ef9a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108691"
---
# <a name="store-encrypted-report-server-data-ssrs-configuration-manager"></a>存储加密的报表服务器数据（SSRS 配置管理器）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 将加密值存储在报表服务器数据库和配置文件中。 大多数加密值都是用于访问向报表提供数据的外部数据源的凭据。 本主题介绍对哪些值进行了加密、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中使用的加密功能以及您应当了解的其他类型的已存储机密数据。  
  
## <a name="encrypted-values"></a>加密值  
 下面列出了 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装中所存储的值。  
  
-   报表服务器用于连接到报表服务器数据库（存储内部服务器数据）的连接信息和凭据。  
  
     这些值是在安装过程中或报表服务器配置期间指定和加密的。 您可以在任何时候使用 Reporting Services 配置工具或 **rsconfig** 实用工具更新连接信息。 对配置设置的加密则是使用对所有用户都可用的本地计算机的计算机级密钥来执行的。 加密的报表服务器连接信息存储在 rsreportserver.config 文件中（其他任何配置文件都不会包含加密设置）。 有关详细信息，请参阅 [配置报表服务器数据库连接（SSRS 配置管理器）](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)中支持的版本。  
  
-   报表服务器用于连接到向报表提供数据的外部数据源的存储凭据。  
  
     这些值是在您为报表配置数据源信息时定义的，随后会以加密值的形式存储在报表服务器数据库中。 报表服务器使用对称密钥对这些数据进行加密和解密。 有关存储的凭据的详细信息，请参阅 [联机丛书中的](../../integration-services/connection-manager/data-sources.md) 为报表数据源指定凭据和连接信息 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   报表服务器用于连接到其他计算机以检索报表中使用的外部图像文件或外部数据的无人参与用户帐户。  
  
     当需要连接到远程计算机且没有其他可用于连接的凭据时，可使用此帐户。 此帐户主要用于支持对不使用凭据即可访问数据源的报表进行无人参与处理。 如果创建报表所依据的数据源在访问数据时不要求或使用凭据，则必须配置此帐户才能使用报表服务器。  
  
     此帐户在某些环境下是必需的，并且只能通过 Reporting Services 配置工具或 **rsconfig**进行创建。 此值还会存储在 rsreportserver.config 文件中。 您必须手动创建此帐户。 有关此帐户及其使用方式的详细信息，请参阅[配置无人参与的执行帐户（SSRS 配置管理器）](configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
-   用于加密的对称密钥。  
  
     此值是在安装过程中或服务器配置期间创建的，随后会以加密值的形式存储在报表服务器数据库中。 报表服务器 Windows 服务使用此密钥对存储在报表服务器数据库中的数据进行加密和解密。  
  
## <a name="encryption-functionality-in-reporting-services"></a>Reporting Services 中的加密功能  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用 Windows 操作系统提供的加密功能。 包括对称加密和非对称加密。  
  
 报表服务器数据库中的数据使用对称密钥进行加密。 每个报表服务器数据库只有一个对称密钥。 此对称密钥使用 Windows 生成的非对称密钥对的公钥进行自加密。 私钥由 Report Server Windows 服务帐户持有。  
  
 在多个报表服务器实例共享同一个报表服务器数据库的报表服务器扩展部署中，所有报表服务器节点都使用一个对称密钥。 每个节点必须具有一个共享对称密钥的副本。 配置扩展部署时，将为每个节点自动创建一个对称密钥副本。 每个节点都使用 Windows 服务帐户专有密钥对的公钥来加密对称密钥的副本。 若要详细了解如何为单个实例和扩展部署创建对称密钥，请参阅[初始化报表服务器（SSRS 配置管理器）](ssrs-encryption-keys-initialize-a-report-server.md)。  
  
> [!NOTE]  
>  如果更改 Report Server Windows 服务帐户，则非对称密钥将变为无效，从而中断服务器操作。 为了避免此类故障，请始终使用 Reporting Services 配置工具来修改服务帐户设置。 使用配置工具时，密钥会自动更新。 有关详细信息，请参阅 [配置报表服务器服务帐户（SSRS 配置管理器）](configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
## <a name="other-sources-of-confidential-data"></a>其他机密数据源  
 报表服务器中还存储有其他可能包含需保护的敏感信息的未加密数据。 具体来说，报表历史记录快照和报表执行快照包含的查询结果可能包括仅供授权用户使用的数据。 因此，对包含机密数据的报表使用快照功能时，需要注意，有权打开报表服务器数据库中的表的用户也能通过检查表的内容来查看所存储报表的部分内容。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 对于所用参数基于用户安全标识的报表，不支持缓存或报表历史记录。  
  
## <a name="see-also"></a>请参阅  
 [配置和管理加密密钥（SSRS 配置管理器）](ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
