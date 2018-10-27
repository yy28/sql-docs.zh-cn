---
title: 远程处理 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d58bcb3c-0b3f-4ab0-81eb-4fdcc86153af
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0afcf50aea6efc0d52adf0b1a82a317e9ec94d08
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146062"
---
# <a name="remote-processing-analysis-services"></a>远程处理 (Analysis Services)
  可在远程 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上运行计划处理或无人参与的处理，其中在一台计算机上发出处理请求，而在同一网络上的另一台计算机上执行该请求。  
  
## <a name="prerequisites"></a>必要條件  
  
-   如果在每台计算机上运行的 SQL Server 版本不同，则客户端库必须与处理模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例版本一致。 例如，如果在 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 实例上进行处理，则发起请求的计算机必须具有与 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]对应的客户端库。 请参阅 [用于 Analysis Services 连接的数据访问接口](../instances/data-providers-used-for-analysis-services-connections.md)。  
  
-   在远程服务器上，必须启用 **“允许远程连接到此计算机”** ，然后必须列出发出处理请求的帐户作为允许的用户。  
  
-   必须配置 Windows 防火墙规则以允许进入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的入站连接。 确认可使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接到远程 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]实例。 请参阅 [Configure the Windows Firewall to Allow Analysis Services Access](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
-   先解决任何现有的本地处理错误，然后再尝试进行远程处理。 确认在处理请求位于本地时，可成功地从外部关系数据源检索数据。 有关指定用于检索数据的凭据的说明，请参阅[设置模拟选项（SSAS-多维）](set-impersonation-options-ssas-multidimensional.md)。  
  
## <a name="on-demand-remote-processing"></a>按需远程处理  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接受从具有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理员权限的用户或应用程序帐户发出的处理请求。 如果您是管理员，请确认您可连接到远程实例并可通过远程连接手动处理数据库。  
  
1.  在将用于安排处理的计算机上，启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 并连接到远程 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。  
  
2.  右键单击数据库，选择“处理”，指向“脚本”，然后选择“将操作脚本保存到‘新建查询’窗口”。 随后将在查询窗口中显示用于调用处理的命令。  
  
3.  单击“确认”  以开始处理。  
  
     成功完成此任务后，将提供一个 XMLA 查询，可将其嵌入计划作业中。 它还确认没有连接问题。  
  
## <a name="schedule-remote-processing-using-sql-server-agent-service"></a>使用 SQL Server 代理服务安排远程处理  
 默认情况下，SQL Server 代理服务在虚拟帐户下运行，其中使用计算机帐户进行网络连接。 若要避免必须向计算机帐户授予对远程 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的管理权限，应更改 SQL Server 代理服务帐户，使其以最低权限的域用户帐户身份运行。  
  
 请务必授予所有必要的权限，包括向帐户 **sysadmin** 授予对提供服务的数据库引擎实例的权限。  
  
 使用以下链接设置权限：  
  
-   [配置 SQL Server 代理](../../ssms/agent/configure-sql-server-agent.md)  
  
-   如果不可能授予[SQL Server Agent Components](../../ssms/agent/sql-server-agent.md#Components) 权限，则 **SQL Server Agent Components** 建议另外的固定服务器角色。  
  
 在配置帐户权限后，请继续进行以下这些步骤。  
  
#### <a name="grant-the-sql-server-agent-account-administrator-permission-on-ssas"></a>向 SQL Server 代理帐户授予对 SSAS 的管理员权限  
  
1.  使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]连接到远程 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。  
  
2.  右键单击服务器名称，单击“属性”，然后单击“安全”。  
  
3.  单击“添加”  以添加 SQL Server 代理帐户。  
  
#### <a name="create-the-job"></a>创建作业  
  
1.  在 Management Studio 中，连接到本地数据库引擎实例。 SQL Server 代理是对象资源管理器中的最后一项。 如有必要，请启动该服务。  
  
2.  右键单击“作业”，单击“新建作业”，然后输入名称。  
  
3.  在“步骤”中，单击“新建”  ，然后输入名称。  
  
4.  在“类型”中，选择“SQL Server Analysis Services 命令” 。  
  
5.  在“服务器”中，输入远程 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。  
  
6.  在“命令”中，粘贴用于处理数据库的 XMLA 命令。 这是在按需远程处理的验证步骤中生成的 XMLA 脚本。 单击 **“确定”** 保存作业。  
  
#### <a name="start-sql-server-profiler"></a>启动 SQL Server Profiler  
  
1.  在远程计算机上，启动 SQL Server Profiler。 连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，然后单击“运行”  以使用默认事件启动跟踪。  
  
     您将使用 SQL Server Profiler 监视所发生的处理事件。  
  
2.  或者，可设置跟踪属性，将跟踪内容发送到数据库内的文件或表中。  
  
#### <a name="run-the-job"></a>运行作业  
  
1.  在用于运行作业的计算机上，确认作业可执行基本操作。 在“对象资源管理器”中的“SQL Server 代理”下，展开“作业”，右键单击刚刚创建的作业，然后单击“作业开始步骤”。 随后立即启动该作业。 可在 SQL Server Profiler 中监视进度。  
  
2.  最后一步，修改该作业，使其按您定义的计划运行，并添加管理作业所需的任何警报或通知。 可能还要细化处理脚本，或在作业中创建多个步骤以独立处理各个对象。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Agent Components](../../ssms/agent/sql-server-agent.md#Components)   
 [使用 SQL Server 代理来计划 SSAS 管理任务](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)   
 [批处理 (Analysis Services)](batch-processing-analysis-services.md)   
 [多维模型对象处理](processing-a-multidimensional-model-analysis-services.md)   
 [处理对象 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)  
  
  
