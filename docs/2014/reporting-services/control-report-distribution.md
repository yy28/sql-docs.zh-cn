---
title: 控制报表分发 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- subscriptions [Reporting Services], e-mail
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- subscriptions [Reporting Services], security
- mail [Reporting Services]
ms.assetid: 8f15e2c6-a647-4b05-a519-1743b5d8654c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: de8a27801ef89f10bf303cee17d1c2d0e1081c5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109701"
---
# <a name="control-report-distribution"></a>控制报表分发
  您可以配置报表服务器，以降低电子邮件和文件共享分发引起的安全风险。  
  
## <a name="securing-reports"></a>保护报表  
 控制报表分发的第一步是保护报表，以防止未经授权的访问。 报表必须使用对所有传递都相同的一组存储凭据，才可以在订阅中使用。 任何可以访问报表服务器上报表的用户都可以运行报表，并且有可能分发报表。 为了防止发生这种情况，您必须限制报表访问，只允许需要报表的用户访问报表。 有关详细信息，请参阅[保护报表和资源](security/secure-reports-and-resources.md)并[保护文件夹](security/secure-folders.md)。  
  
 不能通过订阅的方式分发使用数据库安全性授予访问权限的高度机密报表。  
  
> [!IMPORTANT]  
>  报表以文件的形式传输。 适用于文件的风险和安全措施同样适用于保存到磁盘或以附件形式发送的报表。 具有文件访问权的任何用户都可以根据自己的需要分发或使用相应的文件。  
  
## <a name="controlling-e-mail-delivery"></a>控制电子邮件传递  
 您可以配置报表服务器，使电子邮件分发仅限于特定主机域。 例如，您可以防止报表服务器将报表传递到所有域，而只传递到 RSReportServer 配置文件所列出的域。  
  
 还可以设置配置设置，以在订阅中隐藏 **“收件人”** 字段。 在这种情况下，报表只能传递给定义订阅的用户。 但是，报表发送给用户后，您无法有效地防止转发报表。  
  
 控制报表分发的最有效的方式是，将报表服务器配置为只发送报表服务器 URL。 报表服务器使用 Windows 身份验证和基于角色的授权模型来控制报表的访问权限。 如果用户意外地通过电子邮件收到无权查看的报表，报表服务器不会显示该报表。  
  
## <a name="controlling-file-share-delivery"></a>控制文件共享传递  
 文件共享传递用于将报表发送到硬盘上的文件。 文件保存到磁盘后，就不再受报表服务器用于控制用户访问权限的基于角色安全模式的限制。 若要保护已传递到磁盘的报表，可以对文件本身或报表所在的文件夹设置访问控制列表 (ACL)。 根据您的操作系统情况，可能还会有其他可用的安全选项。  
  
## <a name="see-also"></a>请参阅  
 [为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [订阅和传递 (Reporting Services)](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [创建和管理本机模式报表服务器的订阅](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md)  
  
  
