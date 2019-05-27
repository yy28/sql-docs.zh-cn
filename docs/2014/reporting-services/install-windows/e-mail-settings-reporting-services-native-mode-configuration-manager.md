---
title: 电子邮件设置-配置管理器 （SSRS 本机模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.rsconfigtool.emailsettings.f1
helpviewer_keywords:
- SQL11.rsconfigtool.emailsettings.F1
ms.assetid: cdad1529-bfa6-41fb-9863-d9ff1b802577
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 808ad67429ee49d6b04533863112b4cbb3af2514
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108879"
---
# <a name="e-mail-settings---configuration-manager-ssrs-native-mode"></a>电子邮件设置 - 配置管理器（SSRS 本机模式）
  使用此页可指定简单邮件传输协议 (SMTP) 设置，这些设置用于启用报表服务器的报表服务器电子邮件传递功能。 可使用报表服务器电子邮件传递扩展插件通过电子邮件订阅来分发报表或报表处理通知。 报表服务器电子邮件传递扩展插件需要使用 SMTP 服务器并在“发件人:”字段中使用电子邮件地址。  
  
 其他的配置设置（包括限制邮件服务器主机和呈现扩展插件可用性的设置）可用于进一步自定义电子邮件订阅。 不能在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器中指定这些设置。 若要配置其他设置，必须手动编辑 RSReportServer.config 文件。 有关详细信息，请参阅[为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)并[Reporting Services Configuration Files](../report-server/reporting-services-configuration-files.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]丛书联机。  
  
 若要打开此页，请启动 Reporting Services 配置管理器，并单击**电子邮件设置**在导航窗格中。 有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。  
  
## <a name="options"></a>选项  
 **发件人地址**  
 指定要在所生成电子邮件的“发件人:”字段中使用的电子邮件地址。 您必须指定一个有权从 SMTP 服务器中发送邮件的用户帐户。  
  
 **当前 SMTP 传递方法**  
 指定报表服务器电子邮件通过 SMTP 服务器进行路由。 这是可以在 Reporting Services 配置管理器中指定的唯一传递方法。  
  
 另一种传递方法是使用本地 SMTP 服务拾取目录。 如果网络 SMTP 服务不可用，则可以使用此传递方法。 若要指定本地 SMTP 服务拾取目录，必须编辑 RSReportServer.config 文件。 如果您编辑配置文件以使用本地 SMTP 服务拾取目录，Reporting Services 配置管理器会将 **“传递方法”** 选项设置为“自定义”，以指示传递方法在配置文件中指定。   
  
 在配置文件中，可以通过 `SendUsing` 配置设置来设置传递方法。 有关指定详细信息`SendUsing`设置，请参见[为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。  
  
 **SMTP Server**  
 指定要使用的 SMTP 服务器或网关。 可以使用网络中的本地服务器或 SMTP 服务器。  
  
## <a name="see-also"></a>请参阅  
 [为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [Reporting Services 配置管理器 F1 帮助主题&#40;SSRS 本机模式&#41;](../../sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
  
  
