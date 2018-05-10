---
title: CDC 实例部署脚本 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8fa82822-ac99-48ef-a18d-f4f3a77105b4
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b75dfde662215128c33a7ebf98cf717767d96bd2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="cdc-instance-deployment-script"></a>CDC 实例部署脚本
  显示 CDC 实例部署脚本的“CDC 实例部署脚本”对话框。 此脚本可用于使用其在不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的所有项目重新创建 CDC 数据库。  
  
 在部署脚本完成后，您应该确保以下几个方面：  
  
-   部署脚本假定已通过使用 Oracle CDC 服务配置控制台或通过使用程序创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] “准备脚本” **为 Oracle CDC 准备了目标** 实例。  
  
-   用于启用 CDC 数据库的脚本部分需要由 `sysadmin`运行。  
  
-   该脚本不会保留 Oracle 日志挖掘密码。 该密码需要在脚本已运行并且 Oracle CDC 服务已启动后手动设置。  
  
 在 **“CDC 实例部署脚本”** 对话框中选择以下选项。  
  
 **另存为**  
 将脚本保存在一个文本文件中，您可以将该文本文件保存在所需的任何位置。 您可以将包含该脚本的文件复制到任何其他服务器以便在那里运行脚本。  
  
 **复制**  
 将脚本复制到剪贴板。 然后，您可以将脚本粘贴到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或任何文本编辑器，以便以后运行脚本。  
  
## <a name="see-also"></a>另请参阅  
 [为 CDC 准备 SQL Server](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  
