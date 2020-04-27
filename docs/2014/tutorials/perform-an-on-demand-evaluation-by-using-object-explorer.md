---
title: 使用对象资源管理器执行按需评估 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8d2aadd055334c7ee64871c2fdfe5239c9849e90
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "68210947"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>通过使用对象资源管理器执行按需评估
  在此任务中，您将使用对象资源管理器为 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的单个实例上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]执行最佳实践策略的按需评估。  
  
> [!NOTE]  
>  您还可以通过已注册的服务器评估单个实例上的策略。 有关详细信息，请参阅[使用已注册的服务器执行按需评估](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)。  
  
## <a name="prerequisites"></a>先决条件  
 本课基于 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本。  
  
> [!NOTE]  
>  若要针对正在运行[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]的实例执行最佳实践策略的按需评估，您必须使用主题使用[已注册的服务器执行按需评估](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)主题中所述的过程。  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>通过使用对象资源管理器执行按需评估  
  
1.  启动 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]，然后连接到[!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在对象资源管理器中，依次展开 "**管理**"、"**策略管理**"，右键单击 "**策略**"，然后单击 "**评估**"。  
  
    > [!NOTE]  
    >  默认情况下，本地实例用作策略的源。 如果您以前导入了最佳实践策略，将会列出它们，一起还会列出您已创建的任何其他策略。 你可以选择任何导入的最佳实践策略，然后单击 "**评估**"。 如果您尚未导入最佳实践策略，则继续此过程。  
  
3.  在 "**评估策略**" 对话框中的 "**源**" 框旁，单击省略号（**...**）按钮。  
  
4.  在 "**选择源**" 对话框中，可以选择 "**文件**" 或 "**服务器**" 作为要评估的策略文件的源。 如果单击 "**服务器**"，则可以对以前导入到本地或远程服务器上基于策略的管理的任何最佳实践策略执行按需评估。 在本教程中，您将单击 "**文件**"，然后选择您要评估的各个策略文件。 要实现这一点，请执行下列操作：  
  
    1.  单击 "**文件**"。  
  
    2.  单击 "**文件**" 旁边的省略号（**...**）按钮。  
  
    3.  在 "**选择策略**" 对话框中，浏览到包含最佳实践策略的以下文件夹：  
  
         **C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
        > [!NOTE]  
        >  文件路径可能各不相同，具体取决于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 程序文件的安装位置、运行的操作系统是 32 位还是 64 位以及语言标识符。  
  
    4.  选择要评估的一个或多个 .xml 策略文件，然后单击 "**打开**"。  
  
         所选文件的列表将显示在 "**文件**" 框中。  
  
    5.  在 "**选择源**" 对话框中，单击 **"确定"**。  
  
    6.  如果显示 "**加载策略**" 对话框，则单击 "**关闭**"。  
  
     选择的策略将在 "**策略选择**" 页上列出。 请注意，某一策略旁的警告图标指示该策略包含脚本。  
  
5.  单击 "**评估**" 以评估策略。  
  
     在**结果**表中，将列出每个策略的结果。 红色的“x”图标指示不符合策略。  
  
6.  对于某些策略失败，基于策略的管理使您能够立即对目标强制策略符合。 对于此类失败，在失败的策略旁将出现一个复选框。 如果选中此复选框，"**应用**" 按钮将变为可用。 单击 "**应用**" 时，将在目标实例上自动更新不符合设置。  
  
    > [!CAUTION]  
    >  在自动更新目标实例前，请确保您完全理解该策略设置。 建议你在选中一个或多个复选框后，单击 "**脚本**"，然后选择一个输出位置，以便可以在应用更改[!INCLUDE[tsql](../includes/tsql-md.md)]之前查看基础代码。  
  
7.  若要查看某个策略的详细结果，请在 "**结果**" 表中单击该策略。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [通过使用已注册的服务器执行按需评估](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  
