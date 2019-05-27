---
title: 子包的实现 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- child packages
ms.assetid: ab0c09d7-ce2e-487d-a1ed-a4b5adb6cc01
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1f9eb6860a40f6c47e65beb3fe109255d333d628
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058193"
---
# <a name="implementation-of-child-packages"></a>子包的实现
  使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]来实现负载平衡时，子包将安装在其他服务器上，以利用可用的 CPU 或服务器时间。 若要创建和运行子包，需要执行以下步骤：  
  
-   设计子包。  
  
-   将包移动到远程服务器。  
  
-   在包含运行子包步骤的远程服务器上创建 SQL Server 代理作业。  
  
-   测试并调试 SQL Server 代理作业和子包。  
  
 设计子包时，包的设计不受限制，并且可以添加任何希望的功能。 但是，如果包要访问数据，则必须确保运行包的服务器能够访问该数据。  
  
 若要标识执行子包的父包，请在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的“解决方案资源管理器”中右键单击该包，然后单击“入口点包”。  
  
 设计完子包之后，下一个步骤是将它们部署在远程服务器上。  
  
## <a name="moving-the-child-package-to-the-remote-instance"></a>将子包移动到远程实例  
 将包移动到其他服务器的方式有多个。 两个推荐的方法是：  
  
-   通过使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]将包导出。  
  
-   先为包含要部署的包的项目生成部署实用工具，然后运行包安装向导将包安装到文件系统或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例，从而达到部署包的目的。 有关详细信息，请参阅[包部署&#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)。  
  
 必须重复部署到希望使用的每个远程服务器。  
  
## <a name="creating-the-sql-server-agent-jobs"></a>创建 SQL Server 代理作业  
 子包已经部署到多个服务器之后，请在包含子包的每个服务器上创建 SQL Server 代理作业。 SQL Server 代理作业包含调用作业代理时运行子包的步骤。 SQL Server 代理作业不是已调度作业；它们只在父包调用它们时才会运行子包。 返回到父包的作业成功或失败的通知反映 SQL Server 代理作业成功或失败，以及是否成功调用了代理作业，而不是反映子包的成功或失败或它是否已执行。  
  
## <a name="debugging-the-sql-server-agent-jobs-and-child-packages"></a>调试 SQL Server 代理作业和子包  
 通过使用下列方法之一，可以测试 SQL Server 代理作业及其子包：  
  
-   通过单击“调试” / “开始执行(不调试)”在 SSIS 设计器中运行每个子包。  
  
-   通过使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]在远程计算机上运行单个 SQL Server 代理作业，以确保包运行。  
  
 有关如何对从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理作业运行的包进行故障排除的信息，请参阅 [支持知识库中的](https://support.microsoft.com/kb/918760) An SSIS package does not run when you call the SSIS package from a SQL Server Agent job step [!INCLUDE[msCoName](../includes/msconame-md.md)] （从 SQL Server 代理作业步骤调用 SSIS 包时 SSIS 包不运行）。  
  
 SQL Server 代理检查代理的子系统访问权，并在每次运行作业步骤时将访问权授予代理。  
  
 可以在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中创建代理。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [使用 SQL Server Management Studio 在 SSIS 服务器上运行包](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="related-content"></a>相关内容  
  
-   博客文章[SSIS:访问父包中的变量](https://andyleonard.blog/2015/08/ssis-design-pattern-access-parent-variables-from-a-child-package-in-the-ssis-catalog/)，andyleonard.blog 上。  
  
-   文章中，[执行包任务](../integration-services/control-flow/execute-package-task.md)。  
  
  
