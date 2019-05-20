---
title: 了解本地执行与远程执行之间的差异 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- packages [Integration Services], troubleshooting
ms.assetid: 610ee7d9-4fea-4aba-9395-57add826923b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5a276c1f387e8ebe4b9a2414fcc1d61e6c24a60e
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65718968"
---
# <a name="understanding-the-differences-between-local-and-remote-execution"></a>了解本地执行与远程执行之间的差异

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  包开发人员和管理员应了解与 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包运行位置相关的限制。  
  
-   **包要与启动包的程序运行在同一计算机上。** 即使程序加载的是远程存储于另一台计算机上的包，包也要在本地计算机上运行。  
  
-   **在开发环境外，只可以在安装了 Integration Services 的计算机上运行包。** 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 外，您不能在未安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的客户端计算机上运行包，您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 许可条款可能不允许您在其他计算机上安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 是服务器组件，不可再分发至客户端计算机。 若要从客户端计算机运行包，您需要以可确保包运行于服务器上的方式启动包。  
  
 有关加载和运行已保存的包的详细信息，请参阅：  
  
-   [以编程方式加载和运行本地包](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
  
-   [以编程方式加载和运行远程包](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
 有关运行包并将其输出加载到自定义程序的详细信息，请参阅：  
  
-   [加载本地包的输出](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
## <a name="see-also"></a>另请参阅  
 [以编程方式加载和运行本地包](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [以编程方式加载和运行远程包](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [加载本地包的输出](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
