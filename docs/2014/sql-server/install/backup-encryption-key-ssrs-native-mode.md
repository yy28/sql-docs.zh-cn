---
title: 备份加密密钥 （SSRS 本机模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.backupencryptionkey.F1
ms.assetid: eb8c82be-323b-4d86-ab10-c1bf69a4abe3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: db573e1a070b110ff0f5224a6d079f3fe7c377ca
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061687"
---
# <a name="backup-encryption-key-ssrs-native-mode"></a>备份加密密钥（SSRS 本机模式）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用加密密钥来保护存储在报表服务器数据库中的敏感数据。 备份该密钥对于确保可继续访问连接字符串和凭据至关重要。 如果将报表服务器数据库移动到其他计算机，或者更改报表服务器服务帐户的用户名或密码，则必须备份该密钥。 这两个操作均要求您从先前创建的备份副本还原密钥。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。  
  
 若要打开备份加密密钥对话框中，单击**加密密钥**中的导航窗格[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Configuration Manager，然后单击**备份**。 更新使用服务帐户页中的服务帐户时，也会显示此对话框[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]配置管理器。 有关详细信息[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]配置管理器中，请参阅[Reporting Services 配置管理器&#40;本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>选项  
 **文件位置**  
 指定的文件名和位置[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]到对称密钥。 对称密钥决不能以纯文本形式存储。 您必须键入密码来保护该文件。  
  
 **密码**  
 键入密码以防止对该文件进行未经授权的访问。 只有知道密码的用户才能还原封存在该文件中的密钥。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 强制实施强密码策略。 密码必须至少包含 8 个字符，并且应由大小写字母数字字符和至少一个符号字符组合而成。  
  
 **确认密码**  
 重新键入刚才输入的密码。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 配置管理器 F1 帮助主题&#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [备份和还原 Reporting Services 加密密钥](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [删除和重新创建加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [初始化 Report Server（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [存储加密的 Report Server 数据（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [加密密钥&#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
