---
title: 备份加密密钥（SSRS 本机模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.backupencryptionkey.F1
ms.assetid: eb8c82be-323b-4d86-ab10-c1bf69a4abe3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c8524cdc2c4efb03e2a285c815ca58391045062f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045508"
---
# <a name="backup-encryption-key-ssrs-native-mode"></a>备份加密密钥（SSRS 本机模式）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用加密密钥来保护存储在报表服务器数据库中的敏感数据。 备份该密钥对于确保可继续访问连接字符串和凭据至关重要。 如果将报表服务器数据库移动到其他计算机，或者更改报表服务器服务帐户的用户名或密码，则必须备份该密钥。 这两个操作均要求您从先前创建的备份副本还原密钥。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]本机模式。  
  
 若要打开“备份加密密钥”对话框，请单击 **配置管理器导航窗格中的** “加密密钥” [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，然后单击 **“备份”**。 当使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器中的“服务帐户”页更新服务帐户时，也会显示此对话框。 有关 Configuration Manager 的详细信息 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，请参阅[Reporting Services 配置管理器 &#40;本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>选项  
 **文件位置**  
 为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 指定对称密钥的文件名和位置。 对称密钥决不能以纯文本形式存储。 您必须键入密码来保护该文件。  
  
 **密码**  
 键入密码以防止对该文件进行未经授权的访问。 只有知道密码的用户才能还原封存在该文件中的密钥。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 强制实施强密码策略。 密码必须至少包含 8 个字符，并且应由大小写字母数字字符和至少一个符号字符组合而成。  
  
 **确认密码**  
 重新键入刚才输入的密码。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 配置管理器的 F1 帮助主题 &#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [备份和还原 Reporting Services 加密密钥](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [删除并重新创建 &#40;SSRS Configuration Manager 的加密密钥&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [初始化 Report Server（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [存储加密的 Report Server 数据（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [SSRS 本机模式 &#40;的加密密钥&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
