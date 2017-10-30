---
title: "演练： 设置 SQL Server Integration Services 向外的扩展 |Microsoft 文档"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 685286966599c4dcd3dc2f7029413c77f3ff2689
ms.openlocfilehash: c386b01043764405872365af379cfdedb036b65f
ms.contentlocale: zh-cn
ms.lasthandoff: 10/20/2017

---
# <a name="walkthrough-set-up-integration-services-scale-out"></a>演练：设置 Integration Services Scale Out
设置[!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)]向外扩展通过完成以下任务。 

> [!NOTE]
> 如果你在一台计算机上安装横向扩展，请在同一时间安装缩放出 Master 和横向扩展辅助功能。 同时安装这两种功能时，将自动生成端点以连接到 Scale Out Master。 

* [安装 Scale Out Master](#InstallMaster)

* [安装 Scale Out Worker](#InstallWorker)

* [安装 Scale Out Worker 客户端证书](#InstallCert)

* [打开防火墙端口](#Firewall)

* [启动 SQL Server Scale Out Master 和 Worker 服务](#Start)

* [启用 Scale Out Master](#EnableMaster)

* [启用 SQL Server 身份验证模式](#EnableAuth)

* [启用 Scale Out Worker](#EnableWorker)

## <a name="InstallMaster"></a> 安装 Scale Out Master

若要启用缩放出母版的功能，必须安装数据库引擎服务、 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)]，和你在设置时其缩放出 Master 功能[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 

有关安装数据库引擎服务和 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 的信息，请参阅[安装 SQL Server 数据库引擎](../../database-engine/install-windows/install-sql-server-database-engine.md)和[安装 Integration Services](../install-windows/install-integration-services.md)。
> [!NOTE]
> 若要使用的默认 SQL 身份验证帐户向外扩展日志记录，请在数据库引擎安装过程中针对数据库引擎配置页上的身份验证模式选择混合模式。 请参阅[更改向外扩展日志记录的帐户](change-logdb-account.md)有关详细信息。

**若要安装 Scale Out Master 功能，请使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安装向导或命令提示符。**

- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安装向导的步骤
  1.  上**功能选择**页上，选择**缩放出 Master**，下面列出[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。   
  ![功能选择 Master](media/feature-select-master.PNG)
  
  2.  在“服务器配置”  页上，选择要运行“SQL Server Integration Services Scale Out Master 服务”  的帐户，然后选择“启动类型” 。  
  ![服务器配置](media/server-config.PNG)
  3.  在“Integration Services Scale Out Master 配置”  页上，指定 Scale Out Master 用于与 Scale Out Worker 进行通信的端口号。 默认端口号为 8391。  
  ![主配置](media/master-config.PNG "母版配置")
  4.  指定用于保护出母版横向和横向扩展辅助进程之间的通信通过执行下列其中一项操作的 SSL 证书。
    * 让安装程序创建默认的自签名的 SSL 证书通过单击**创建新的 SSL 证书**。  默认证书安装在本地计算机中受信任的根证书颁发机构之下。 你可以指定在此证书的 Cn。 主终结点的主机名应包含在 Cn。 默认情况下，将包含计算机名称和主节点的 ip。
    * 通过单击选择本地计算机上的现有 SSL 证书**使用现有的 SSL 证书**，然后单击**浏览**选择证书。 文本框中显示证书的指纹。 单击“浏览”  ，显示存储在本地计算机中受信任的根证书颁发机构中的证书。 必须选择存储在此处的证书。       
![主配置 2](media/master-config-2.PNG "Master 配置 2")
  5.  完成 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安装向导。
- 命令提示符的步骤

    按照[从命令提示符安装 SQL Server](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) 中的说明操作。 执行以下操作，设置 Scale Out Master 的相关参数。
  1.  将 IS_Master 添加到参数 /FEATURES
  2.  将缩放出主机配置为通过指定以下参数和它们的值： /ISMASTERSVCACCOUNT、 /ISMASTERSVCPASSWORD、 /ISMASTERSVCSTARTUPTYPE、 /ISMASTERSVCPORT，/ISMasterSVCSSLCertCN(optional)、 /ISMASTERSVCTHUMBPRINT(optional)。

> [!Note]
> 如果缩放出 Master 不与数据库引擎一起安装，并且数据库引擎是命名的实例，你需要安装后在缩放出 Master 服务配置文件中配置 SqlServerName。 请参阅[缩放出 Master](integration-services-ssis-scale-out-master.md)有关详细信息。

## <a name="InstallWorker"></a> 安装 Scale Out Worker
 
若要启用 Scale Out Worker 的功能，必须在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安装程序中安装 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 及其 Scale Out Worker 功能。

**若要安装 Scale Out Worker 功能，请使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安装向导或命令提示符。**

- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安装向导的步骤
  1.  上**功能选择**页上，选择**横向扩展辅助**，下面列出[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。   
  ![功能选择 Worker](media/feature-select-worker.PNG)
  2. 在“服务器配置”  页上，选择要运行“SQL Server Integration Services Scale Out Worker 服务”  的帐户，然后选择“启动类型” 。    
  ![服务器配置 2](media/server-config-2.PNG "服务器配置 2")
  3. 在“Integration Services Scale Out Worker 配置”  页上，指定端点以连接到 Scale Out Master。 
      > [!Note]
      > 可以此处跳过辅助节点配置 （步骤 3 和 4） 并将关联到与缩放出母版出辅助缩放[缩放出 Manager](integration-services-ssis-scale-out-manager.md)在安装完成后。

    - 有关**一台计算机**缩放出 Master 和横向扩展辅助安装在同一时间时，将自动生成环境中，终结点。 
    - 有关**多台计算机**环境中，终结点组成的名称或计算机的 IP 与安装 Master 出横向和横向扩展 Master 安装过程中指定的端口号。    
   ![辅助进程配置 1](media/worker-config.PNG "辅助配置 1")    

  4. 有关**多台计算机**环境中，指定用于验证缩放出母版的客户端 SSL 证书。 有关**一台计算机**环境，无需指定客户端 SSL 证书。 
  
     > [!NOTE]
     > 自签名由缩放出主机使用的 SSL 证书时，相应的客户端 SSL 证书时需要安装在横向扩展辅助计算机上。 如果你的文件路径为客户端提供 SSL 证书上**Integration Services 辅助配置出缩放**页上，该证书将自动安装; 否则，你必须手动更高版本安装证书。 
     
     单击“浏览”  ，查找证书文件 (*.cer)。 若要使用的默认 SSL 证书，选择位于 SSISScaleOutMaster.cer 文件\<驱动器\>: files\microsoft SQL Server\140\DTS\Binn 缩放出母版安装在其的计算机上。   
   ![辅助进程配置 2](media/worker-config-2.PNG "辅助配置 2")
  5. 完成 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安装向导。
- 命令提示符的步骤

    按照[从命令提示符安装 SQL Server](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) 中的说明操作。 执行以下操作，设置 Scale Out Worker 的相关参数。
    1.  将 IS_Worker 添加到参数 /FEATURES
    2. 配置横向扩展辅助指定以下参数和它们的值： /ISWORKERSVCACCOUNT、 /ISWORKERSVCPASSWORD、 /ISWORKERSVCSTARTUPTYPE，/ISWORKERSVCMASTER(optional)、 /ISWORKERSVCCERT(optional)。

 
## <a name="InstallCert"></a> 装 Scale Out Worker 客户端证书

安装过程中的横向扩展辅助进程的工作线程证书将自动创建，并在计算机上安装。 此外，将在 \<driver\>:\Program Files\Microsoft SQL Server\140\DTS\Binn 之下安装相应的客户端证书 SSISScaleOutWorker.cer。 对于横向出母版进行横向扩展辅助身份验证，必须将此客户端证书添加到缩放出 Master 的本地计算机的根存储区。
  
若要将客户端证书添加到根存储，可双击 .cer 文件，然后单击“证书”对话框中的“安装证书”  。 将显示“证书导入向导”  。  

## <a name="Firewall"></a>打开防火墙端口

打开在缩放出主安装和端口的 SQL Server (1433，默认情况下)，过程中指定的端口在缩放出主计算机上使用 Windows 防火墙。
    
## <a name="Start"></a>启动 SQL Server Scale Out Master 和 Worker 服务

如果在安装过程中服务的启动类型未设置为自动，启动服务： SQL Server Integration Services 缩放出 Master 14.0 (SSISScaleOutMaster140) 和 SQL Server Integration Services 缩放出辅助 14.0 (SSISScaleOutWorker140)。 

> [!Note]
> 打开防火墙端口后，你还需要重新启动了缩放出 Worker 服务。
   
## <a name="EnableMaster"></a> 启用 Scale Out Master

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)] 中创建 SSISDB 目录时，请在“创建目录”对话框中，单击“启用此服务器作为 SSIS Scale Out Master”。 或者，可以使用启用缩放出 Master[缩放出 Manager](integration-services-ssis-scale-out-manager.md)创建目录后。

## <a name="EnableAuth"></a> 启用 SQL Server 身份验证模式
如果[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]身份验证未启用数据库引擎安装期间上, 启用 SQL Server 身份验证模式[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]承载 SSISDB 目录的实例。 

禁用 SQL Server 身份验证时，包执行不会受到阻止。 但是，执行日志将无法写入 SSISDB。

## <a name="EnableWorker"></a> 启用 Scale Out Worker

可以通过启用横向扩展辅助[缩放出 Manager](integration-services-ssis-scale-out-manager.md)、 提供 GUI; 或通过存储过程启用，请参阅下文。

若要启用 Scale Out Worker，请以 *WorkerAgentId* 作为参数，执行 **[catalog].[enable_worker_agent]** 存储过程。 

Scale Out Worker 注册到 Scale Out Master 之后，将从 SSISDB 的 **[catalog].[worker_agents]** 数据库视图中获取 *WorkerAgentId* 值。 Scale Out Master 和 Worker 服务启用之后，需要花几分钟进行注册。

#### <a name="example"></a>示例
此示例将启用辅助计算机 a 上缩放出。
```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName  --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    computerA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```
## <a name="next-steps"></a>后续步骤
已完成 Scale Out 功能的设置。 你现在可以在向外扩展运行包。有关详细信息，请参阅[在 Integration Services (SSIS) Scale Out 中执行包](run-packages-in-integration-services-ssis-scale-out.md)。
