---
title: 加密密钥 （SSRS 本机模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.encryptionkeypanel.F1
ms.assetid: cc7e6f84-80e1-4b5e-9409-d0e074edd147
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 16ac264f89c541f0a864f8b47ed008fa254f181c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66095418"
---
# <a name="encryption-keys-ssrs-native-mode"></a>加密密钥（SSRS 本机模式）
  使用“加密密钥”页可以管理用于对报表服务器中数据进行加密和解密的对称密钥。 管理加密密钥是报表服务器配置的一个重要方面。 在创建报表服务器数据库时，自动创建并应用对称密钥。 创建对称密钥的备份副本，以便您可以执行例行的维护操作。 您需要具有对称密钥的有效副本，才可执行以下维护任务：  
  
-   更改报表服务器服务的服务帐户。  
  
-   将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装迁移到其他计算机。  
  
-   配置新的报表服务器实例以共享或使用现有报表服务器数据库。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。  
  
> [!IMPORTANT]  
>  定期更改 Reporting Services 加密密钥是确保安全的好办法。 建议在升级 Reporting Services 主版本后立即更改密钥。 升级后更改密钥将使在升级周期外更改 Reporting Services 加密密钥所导致的额外服务中断降到最低程度。  
  
 如果更新了报表服务器服务的用户帐户（并且是使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器以外的工具更改了此帐户），或者要将报表服务器安装迁移到新服务器，则必须还原对称密钥。  
  
 为了保护对称密钥免受未经授权的访问，对称密钥使用报表服务器服务的私钥进行了加密。 只有报表服务器服务可以解锁并使用对称密钥以在报表服务器数据库中存储敏感数据。 如果更改了报表服务器服务的标识，或者将报表服务器迁移到新计算机，则报表服务器服务的私钥将不再能够解开对称密钥的锁定。 若要恢复对对称密钥的访问，请使用新报表服务器服务标识的私钥重新加密对称密钥。 还原对称密钥就是对对称密钥重新加密的过程。  
  
 只还原当前用于加密和解密报表服务器数据库中数据的对称密钥。 如果还原无效的对称密钥，您将不再能够访问敏感数据。 在这种情况下，必须删除并重新创建密钥。  
  
> [!IMPORTANT]  
>  删除和重新创建对称密钥的操作不能逆转或撤消。 删除或重新创建该密钥可能对您当前的安装产生重要影响。 如果删除对称密钥，则使用此密钥加密的所有现有数据也将被删除。 删除的数据包括指向外部报表数据源的连接字符串、存储的连接字符串和某些订阅信息。  
  
 若要打开此页，请启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器，然后在导航窗格中选择相应链接。 有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>选项  
 **备份**  
 将对称密钥复制到您指定的文件。 对称密钥决不能以纯文本形式存储。 您必须键入密码来保护该文件。  
  
 **还原**  
 将以前保存的对称密钥的副本应用于报表服务器数据库。 您必须提供密码对文件进行解锁。  
  
 还原后的对称密钥副本将覆盖当前连接的报表服务器实例还原前的对称密钥副本。 还原对称密钥后，必须初始化使用该报表服务器数据库的所有报表服务器。 有关初始化报表服务器的详细信息，请参阅[初始化报表服务器&#40;SSRS 配置管理器&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)。  
  
 **更改**  
 重新创建对称密钥并对报表服务器数据库中的所有加密值重新进行加密。 请确保在重新创建对称密钥前停止报表服务器服务。  
  
 在扩展部署中，对称密钥的所有副本都将替换为新的版本。 在更改对称密钥前，请务必检查加入扩展部署的服务器的列表，以确认仅对有效的报表服务器实例授予了对新密钥的访问权限。 “扩展部署”页列出了扩展部署中包含的服务器  。 在重新创建密钥前，请停止部署中包含的各个报表服务器上的报表服务器服务。  
  
 请注意，如果您具有许多数据源和订阅，则重新生成对称密钥的过程可能需要耗费较长的时间。  
  
 **删除**  
 删除对称密钥和所有加密内容（包括连接字符串和存储的凭据）。 如果您无法还原对称密钥，则只能删除该密钥。  
  
 一旦删除了对称密钥，您必须在报表和共享数据源中重新输入缺少的连接字符串和存储的凭据，因为其中已不再具有这些值。 另外，对于使用存储加密数据的传递扩展插件的所有订阅，还必须进行更新。 这包括使用加密值的文件共享传递扩展插件和任何第三方传递扩展插件。  
  
 此信息无法自动更新。 一次只能更新一个使用存储的凭据和连接字符串的报表、订阅和共享数据源。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 配置管理器 F1 帮助主题&#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [备份和还原 Reporting Services 加密密钥](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [删除和重新创建加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [初始化 Report Server（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [存储加密的 Report Server 数据（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
