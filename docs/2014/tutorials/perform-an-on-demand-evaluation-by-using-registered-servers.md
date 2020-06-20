---
title: 使用已注册的服务器执行按需评估 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: c14034ef-6e0b-4df5-8072-bfb8d90b3172
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e3ffcef923eaeb3ba48eacaca870bd3355fb6661
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85035577"
---
# <a name="perform-an-on-demand-evaluation-by-using-registered-servers"></a>通过使用已注册的服务器执行按需评估

  您可以通过使用已注册的服务器对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的一个或多个实例执行最佳实践策略的按需评估。 您可以使用本地服务器组或中央管理服务器。  
  
> [!NOTE]  
>  您可以对运行 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 或者 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的更高版本的服务器组成员执行最佳实践策略的按需评估。 但是，如果存在引用在 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 或 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)] 中不支持的策略的一些属性，则您可能会接收异常错误。  
  
## <a name="prerequisites"></a>先决条件  
 要执行此任务，您必须在已注册的服务器中已配置一个或多个服务器注册。 有关详细信息，请参阅下列主题：  
  
-   [创建或编辑服务器组 (SQL Server Management Studio)](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [&#40;SQL Server Management Studio&#41;注册连接的服务器](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md)。  
  
-   [创建中央管理服务器和服务器组 (SQL Server Management Studio)](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-evaluate-best-practices-policies-against-a-server-group"></a>对于服务器组执行最佳实践策略  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中的 **“视图”** 菜单上，单击 **“已注册的服务器”**。  
  
2.  展开 "**数据库引擎**"，然后展开 "**本地服务器组**" 或 "**中央管理服务器**"，具体取决于你的配置。  
  
3.  执行下列任一操作：  
  
    -   若要针对本地服务器组或中央管理服务器管理的所有服务器评估策略，请右键单击本地服务器组名称或中央管理服务器名称，然后单击 "**评估策略**"。  
  
        > [!NOTE]  
        >  在通过中央管理服务器评估策略时，不对中央管理服务器本身评估策略。  
  
    -   若要针对特定服务器或服务器组评估策略，请展开 "**本地服务器组**" 或 "中央管理服务器名称"，右键单击要评估策略的服务器或服务器组，然后单击 "**评估策略**"。  
  
4.  在 "**评估策略**" 对话框中的 "**源**" 框旁，单击省略号（**...**）按钮。  
  
5.  在 "**选择源**" 对话框中，可以选择 "**文件**" 或 "**服务器**" 作为要评估的策略文件的源。 如果单击 "**服务器**"，则可以对以前导入到本地或远程服务器上基于策略的管理的任何最佳实践策略执行按需评估。 在本教程中，您将单击 "**文件**"，然后选择您要评估的各个策略文件。 为此，请按照下列步骤进行操作：  
  
    1.  单击 "**文件**"。  
  
    2.  单击 "**文件**" 旁边的省略号（**...**）按钮。  
  
    3.  选择要评估的一个或多个 .xml 策略文件，然后单击 "**打开**"。  
  
         所选文件的列表将显示在 "**文件**" 框中。  
  
    4.  在 "**选择源**" 对话框中，单击 **"确定"**。  
  
    5.  如果显示 "**加载策略**" 对话框，则单击 "**关闭**"。  
  
     选择的策略将在 "**策略选择**" 页上列出。 请注意，某一策略旁的警告图标指示该策略包含脚本。  
  
6.  单击 "**评估**" 以评估策略。  
  
7.  对于某些策略失败，基于策略的管理使您能够立即对目标强制策略符合。 对于此类失败，在失败的策略旁将出现一个复选框。 如果选中该复选框，或单击具有失败策略的行，则复选框将出现在 "**目标详细信息**" 窗格中的 "目标详细信息" 窗格中。 如果选中任何复选框，"**应用**" 按钮将变为可用。 单击 "**应用**" 时，不符合性设置将在你选择的目标实例上自动更新。  
  
    > [!CAUTION]  
    >  在自动更新目标实例前，请确保您完全理解该策略设置。 建议你在选中一个或多个复选框后，单击 "**脚本**"，然后选择一个输出位置，以便可以在 [!INCLUDE[tsql](../includes/tsql-md.md)] 应用更改之前查看基础代码。  
  
8.  若要查看某个策略的详细结果，请在 "**结果**" 表中单击该策略。 "**目标详细信息**" 表显示每个实例的详细信息。  
  
## <a name="next-lesson"></a>下一课  
 [第 2 课：定期评估最佳做法策略](../../2014/tutorials/lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制实施最佳实践](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)   
 [使用中央管理服务器管理多台服务器](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
