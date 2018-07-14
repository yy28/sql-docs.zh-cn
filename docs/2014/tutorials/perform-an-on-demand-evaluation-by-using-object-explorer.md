---
title: 通过使用对象资源管理器执行按需评估 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
caps.latest.revision: 8
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 95ce7493353fbce70ec10f575b7a637ea4d8809c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237927"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>通过使用对象资源管理器执行按需评估
  在此任务中，您将使用对象资源管理器为 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的单个实例上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]执行最佳实践策略的按需评估。  
  
> [!NOTE]  
>  您还可以通过已注册的服务器评估单个实例上的策略。 有关详细信息，请参阅[执行按需评估使用已注册的服务器通过](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)。  
  
## <a name="prerequisites"></a>必要條件  
 本课基于 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本。  
  
> [!NOTE]  
>  若要执行对正在运行的实例的最佳实践策略的按需评估[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]，你必须使用本主题中的过程[执行按需评估使用已注册的服务器通过](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)。  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>通过使用对象资源管理器执行按需评估  
  
1.  启动 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]，然后连接到[!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在对象资源管理器，展开**管理**，展开**策略管理**，右键单击**策略**，然后单击**评估**。  
  
    > [!NOTE]  
    >  默认情况下，本地实例用作策略的源。 如果您以前导入了最佳实践策略，将会列出它们，一起还会列出您已创建的任何其他策略。 您可以选择任何导入的最佳实践策略，然后单击**Evaluate**。 如果您尚未导入最佳实践策略，则继续此过程。  
  
3.  在中**评估策略**对话框旁边**源**框中，单击省略号 (**...**) 按钮。  
  
4.  在中**选择源**对话框中，您可以选择**文件**或**Server**作为要评估的策略文件的源。 如果单击**Server**，可以执行任何以前导入到本地或远程服务器上的基于策略的管理的最佳实践策略的按需评估。 您将在本教程中，单击**文件**，然后选择你想要评估的单独的策略文件。 为此，请按照下列步骤进行操作：  
  
    1.  单击**文件**。  
  
    2.  下一步**文件**，单击省略号 (**...**) 按钮。  
  
    3.  在中**选择策略**对话框中，浏览到包含最佳实践策略的以下文件夹：  
  
         **C:\Program 文件 (x86) \Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
        > [!NOTE]  
        >  文件路径可能各不相同，具体取决于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 程序文件的安装位置、运行的操作系统是 32 位还是 64 位以及语言标识符。  
  
    4.  选择要评估，然后依次的一个或多个.xml 策略文件**打开**。  
  
         所选文件的列表将显示在**文件**框。  
  
    5.  在中**选择源**对话框中，单击**确定**。  
  
    6.  如果**加载策略**出现对话框，请单击**关闭**。  
  
     上列出所选的策略**策略选择**页。 请注意，某一策略旁的警告图标指示该策略包含脚本。  
  
5.  单击**Evaluate**来评估策略。  
  
     在中**结果**表，结果列出了每个策略。 红色的“x”图标指示不符合策略。  
  
6.  对于某些策略失败，基于策略的管理使您能够立即对目标强制策略符合。 对于此类失败，在失败的策略旁将出现一个复选框。 如果选择该复选框，**应用**按钮将变为可用。 当您单击**应用**，将目标实例上自动更新不符合要求的设置。  
  
    > [!CAUTION]  
    >  在自动更新目标实例前，请确保您完全理解该策略设置。 我们建议，选择一个或多个复选框后，单击**脚本**，然后选择输出位置，以便你可以查看基础[!INCLUDE[tsql](../includes/tsql-md.md)]代码之前应用所做的更改。  
  
7.  若要查看某个策略的详细的结果，请单击中的策略**结果**表。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [通过使用已注册的服务器执行按需评估](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  
