---
title: 还原加密密钥（SSRS 本机模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.restoreencryptionkey.F1
ms.assetid: 11ce51e5-f5d4-40b6-88d8-9360fb50e66c
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 111e44275922149949cd7e252e112d95cef65076
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952033"
---
# <a name="restore-encryption-key-ssrs-native-mode"></a>还原加密密钥（SSRS 本机模式）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用加密密钥来保护存储在报表服务器数据库中的敏感数据。 为确保您可以继续访问加密数据，请务必创建加密密钥的备份，以备以后因服务帐户发生变化而需要还原它或需要将它作为计划迁移的一部分还原时使用。 本主题概括了如何使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器来还原密钥。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。  
  
 若要还原此密钥，事先必须将此密钥的备份副本保存到受密码保护的文件中。 在密钥还原过程中，报表服务器将用在受密码保护的文件中找到的密钥替换现有密钥。 该文件中的密钥必须与用于加密和解密数据的密钥相同。  
  
 若要验证是否还原了有效的密钥，请使用报表管理器来查看订阅或具有使用存储凭据的数据源的任何报表。 如果在试图打开订阅定义页时出现“报表服务器无法访问加密数据”错误，或者在打开此前将存储凭据用于报表数据源的报表时，系统提示您输入凭据，则表明您还原的是无效密钥。  
  
 如果还原的是无效密钥，而不是用于加密数据的密钥，则无法解密当前存储在报表服务器数据库中的数据。 如果还原的是无效密钥，则应立即还原正确密钥的备份副本（如果有的话）。 如果没有用于加密数据的密钥的备份副本，则必须删除所有加密数据。 请单击 **加密密钥** 页上的 [“删除”](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md) 按钮以执行此步骤。 在删除加密内容之后，必须手动更新所有订阅并重新指定为报表定义的所有存储凭据以及报表服务器上的所有数据驱动订阅。  
  
## <a name="restore-encryption-key-dialog"></a>“还原加密密钥”对话框  
 有关在何处查找 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager 的信息，请参阅[Reporting Services 配置管理器&#40;本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
 若要打开“还原加密密钥”对话框，请单击 **配置管理器导航窗格中的** “加密密钥” [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，然后单击 **“还原”** 。 当使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器中的“服务帐户”页更新服务帐户时，也会显示此对话框。 有关更多信息  
  
## <a name="options"></a>“常规”  
 **文件位置**  
 选择包含对称密钥副本的受密码保护的文件。 默认的文件扩展名为 .snk。  
  
 **密码**  
 输入用于解锁该文件的密码。 只有知道密码的用户才可还原密钥。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 强制实施强密码策略。 密码必须至少包含 8 个字符，并且应由大小写字母数字字符和至少一个符号字符组合而成。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 配置管理器 F1 帮助主题&#40;SSRS 本机模式&#41; ](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [备份和还原 Reporting Services 加密密钥](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [删除和重新创建加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [初始化 Report Server（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [存储加密的 Report Server 数据（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [加密密钥&#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
