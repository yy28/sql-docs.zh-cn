---
title: "了解本地和远程执行之间的差异 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- packages [Integration Services], troubleshooting
ms.assetid: 610ee7d9-4fea-4aba-9395-57add826923b
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1921a7760e42f101ebf5d9b898972c2b2ab8173b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="understanding-the-differences-between-local-and-remote-execution"></a>了解本地执行与远程执行之间的差异
  包开发人员和管理员应了解与 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包运行位置相关的限制。  
  
-   **将它启动的程序所在的同一计算机上运行的包**。 即使程序加载的是远程存储于另一台计算机上的包，包也要在本地计算机上运行。  
  
-   **您可以仅运行已安装的 Integration Services 的计算机上的开发环境外部包**。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 外，您不能在未安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的客户端计算机上运行包，您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 许可条款可能不允许您在其他计算机上安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]是服务器组件而不是向客户端计算机可再发行组件。 若要从客户端计算机运行包，您需要以可确保包运行于服务器上的方式启动包。  
  
 有关加载和运行已保存的包的详细信息，请参阅：  
  
-   [以编程方式加载和运行本地包](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
  
-   [以编程方式加载和运行远程包](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
 有关运行包并将其输出加载到自定义程序的详细信息，请参阅：  
  
-   [加载本地包的输出](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
## <a name="see-also"></a>另请参阅  
 [加载和以编程方式运行本地包](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [加载和以编程方式运行远程包](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [加载本地包的输出](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
