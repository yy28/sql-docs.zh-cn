---
title: 升级包（SSIS 包升级向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.upgradingpackage.f1
ms.assetid: cdb842e3-2e59-4ede-b127-be4fde46875c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 95c4a27a6ef20ac52521c707ae4a83329a81716d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972657"
---
# <a name="upgrading-the-packages-ssis-package-upgrade-wizard"></a>升级包（SSIS 包升级向导）
  可以使用 **“升级包”** 页查看包升级的进度以及中断升级过程。 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包升级向导会逐一升级所选包。  
  
 **查看保存到 SQL Server 数据库或包存储区的升级包**  
  
-   在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]中的对象资源管理器中，连接到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的本地实例，然后展开 **“已存储的包”** 节点查看已升级的包。  
  
 **查看通过 SQL Server Data Tools 升级的升级包**  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中的解决方案资源管理器中，打开 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目，然后展开 **“SSIS 包”** 节点查看已升级的包。  
  
## <a name="options"></a>选项  
 **消息窗格**  
 在升级过程中显示进度消息和摘要信息。  
  
 **操作**  
 查看升级中的操作。  
  
 **状态**  
 查看每个操作的结果。  
  
 **Message**  
 查看每个操作生成的错误消息。  
  
 **Stop**  
 停止包升级。  
  
 **Report**  
 选择希望如何处理包含包升级结果的报告：  
  
-   联机查看报告。  
  
-   将报告保存到文件中。  
  
-   将报告复制到剪贴板  
  
-   将报告作为电子邮件发送。  
  
## <a name="see-also"></a>另请参阅  
 [升级 Integration Services 包](install-windows/upgrade-integration-services-packages.md)  
  
  
