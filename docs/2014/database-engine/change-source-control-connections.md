---
title: 更改源代码管理连接 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server Management Studio], source controls
- source controls [SQL Server Management Studio], connections
ms.assetid: 538e3beb-f99c-4095-bd65-6413e872d26e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d57f5938cb888a955645f5a9e0b01eeacfc1142b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62812786"
---
# <a name="change-source-control-connections"></a>更改源代码管理连接
  第一次从源代码管理中添加或打开解决方案时，源代码管理提供程序会在本地解决方案目录的根文件夹与对应的服务器文件夹之间创建一个关联。  
  
 根文件夹（还称为统一根）位于客户端。 由解决方案或项目引用的所有文件均可在此文件夹下找到。 若要找到解决方案的最新版本、历史记录及其状态信息，请找到驻留在源代码管理服务器上的服务器文件夹。 在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 中，服务器文件夹被称为项目。  
  
 多数情况下，需要将解决方案与其服务器文件夹解除绑定或断开连接。 例如，如果您的源代码管理提供程序所在的计算机无法使用，则可以连接到备份计算机，将解决方案重新绑定到备份的服务器文件夹，然后继续正常工作。 而且，如果源代码管理项目是派生的，则可能需要将解决方案绑定到新项目版本所在的服务器文件夹。  
  
 使用源代码管理提供程序的用户界面来更改与解决方案绑定的服务器文件夹。 可以从 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 环境内打开源代码管理用户界面。  
  
#### <a name="to-open-the-source-control-user-interface-from-the-studio-environment"></a>从 Studio 环境中打开源代码管理用户界面  
  
1.  上**文件**菜单，依次指向**源代码管理**，然后单击**启动 Microsoft Visual SourceSafe**。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理基础知识](../../2014/database-engine/source-control-basics.md)   
 [设置源代码管理选项](../../2014/database-engine/set-source-control-options.md)   
 [从源代码管理中排除文件](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
