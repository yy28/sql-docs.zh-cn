---
title: "在无法访问 Internet 的情况下安装 R 组件 | Microsoft Docs"
ms.custom: 
ms.date: 02/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 30
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 15d5426b1024d573b77aa02d5b29370ebfeb5d4c
ms.lasthandoff: 04/11/2017

---
# <a name="installing-r-components-without-internet-access"></a>在无法访问 Internet 的情况下安装 R 组件
本主题介绍如何获取脱机安装 SQL Server R Services 所需的 R 组件安装文件，以及如何在交互式 SQL Server 安装过程中安装这些组件。

通常，安装 SQL Server R Services 中使用的 R 组件需要连接到 Internet。 由于某些组件和库是开放源代码，Microsoft 默认不会安装它们，但为方便起见，在 Microsoft 下载中心和其他受信任站点上提供了相关的安装程序。

> [!TIP]
> 
> 有关脱机安装过程的分步演练和屏幕截图，请参阅 [SQL Server 客户顾问团队](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)撰写的这篇文章。 此文还介绍了修补和补充安装方案。
  

## <a name="1-obtain-r-component-installation-files"></a>1.获取 R 组件安装文件

R 组件有两个安装程序：一个适用于 Microsoft R Open (SRO)，另一个适用于 Microsoft R Server 和数据库组件 (SRS)。 必须同时下载并安装这两个程序，才能使用 SQL Server R Services。 使用 SQL Server 安装向导可以确保按正确的顺序安装它们。

  
1. 从 [Microsoft 下载中心站点](#installerlocs)将安装程序下载到可以访问 Internet 的计算机，此时请选择保存安装程序，而不要运行它。 请务必获取与所要安装的 SQL Server 版本匹配的文件。
2. 将安装程序 (CAB) 文件复制到用于安装 R Services 的计算机。  
3. 如果安装的语言不是默认语言，请根据以下部分中所述修改安装程序文件名：[根据不同的语言区域设置进行修改](#modslocales)。
4. 也可以针对开放源代码组件下载存档源代码。 有关详细信息，请参阅 [安装 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。

## <a name="2-install-r-services-offline-using-the-sql-server-setup-wizard"></a>2.使用 SQL Server 安装向导脱机安装 R Services  

5. 运行 SQL Server 安装向导。
6. 当安装向导显示 Microsoft R Open 许可页时，请单击“接受”。  
7. 此时将打开一个对话框，提示输入 Microsoft R Open 和 Microsoft R Server 包的“安装路径”。
输入已下载文件的位置路径。 
8. 单击“浏览”找到包含前面复制的安装程序文件的文件夹。
9. 如果找到了正确的文件，可以单击“下一步”指示相应的组件可用。
10. 完成 SQL Server 安装向导。
11. 根据以下主题中所述执行安装后步骤：[Set Up SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)（设置 SQL Server R Services）

## <a name="installerlocs"></a>R 组件安装程序的链接

发行版本  |下载链接  
---------|---------
**SQL Server 2016 RTM**     |           
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)     
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)      
**SQL Server 2016 CU 1**     |           
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)     
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)      
**SQL Server 2016 CU 2**     |           
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)     
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)  
**SQL Server 2016 CU 3**     |           
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)     
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)  |
**SQL Server 2016 SP 1**     |           
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)     
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)  
**SQL Server 2016 SP 1 GDR**     |           
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)     
Microsoft R Server     |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)  
**SQL Server vNext CTP 1**     |           
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)     
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)  
**SQL Server vNext CTP 1.1** |           
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)     
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)  
**SQL Server vNext CTP 1.4** |           
Microsoft R Open     |[SRO_3.3.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)     
Microsoft R Server     |[SRS_9.0.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)    
 
## <a name="modslocales"></a>根据不同的语言区域设置进行修改

在连接了 Internet 的计算机上，如果在安装 SQL Server 的过程中下载了 cab 文件，安装向导会检测本地语言并自动更改安装程序的语言。 

但是，如果在未连接 Internet 的计算机上安装某个本地化版本的 SQL Server，并且将 R 安装程序下载到本地共享，则必须手动编辑所下载文件的名称，并为正在安装的语言插入正确的语言标识符。 

 
例如，如果安装日语版 SQL Server，应将文件名称从 SRS_8.0.3.0_**1033**.cab 更改为 SRS_8.0.3.0_**1041**.cab。    
 
### <a name="additional-prerequisites"></a>其他必备组件

根据所用的环境，可能需要为以下必备组件创建安装程序的本地副本。  


组件  |版本   
---------|---------
[Microsoft AS OLE DB Provider for SQL Server 2016](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5         
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1          
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25          
[Microsoft Visual C++ 2013 Redistributable](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0         
[Microsoft Visual C++ 2015 Redistributable](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0         

  


## <a name="support-for-slipstream-upgrades"></a>支持补充升级

补充安装是指对失败的实例安装应用修补或更新，以修复现有的问题。 此方法的优点在于，可以在执行安装的同时更新 SQL Server，避免以后单独重新启动。

+ 在 SQL Server 2016 中，可以通过单击 SQL Server Management Studio 中的“工具”，然后选择“检查更新”来启动补充升级。 也可以在命令提示符中键入 **SETUP.EXE** 来启动 SQL Server 安装实用工具。

+ 如果服务器无法访问 Internet，则在开始执行更新过程**之前**，必须下载 SQL Server 安装程序，然后下载 R 组件安装程序的匹配版本。  SQL Server 默认未随附 R 组件，因为这些组件包含单独许可的开放源代码软件。 

如果要将 R Services 添加到以前安装的实例，请使用 SQL Server 安装程序的更新版本，以及 R 组件的相应更新版本。 当你指定安装 R 功能时，安装程序将查找 R CAB 文件的匹配版本。 

## <a name="command-line-arguments-for-offline-unattended-upgrades"></a>用于脱机无人参与升级的命令行参数

执行无人参与的安装时，请使用以下命令行参数指定安装程序的位置：
- 使用 */UPDATESOURCE* 指定包含 SQL Server 更新安装程序的文件本地的位置  
- 使用 */MRCACHEDIRECTORY* 指定包含 R 组件 CAB 文件的文件夹
- 使用 */IACCEPTROPENLICENSETERMS="True"* 接受单独提供的 R 许可协议 

    
> [!TIP]
> 有关无人参与的安装和升级方案的其他信息（包括示例脚本），请参阅 R Services 支持团队撰写的以下博客文章：[Deploying R Services on Computers without Internet Access](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)（无法访问 Internet 的情况下在计算机上部署 R Services）。

## <a name="see-also"></a>另请参阅  
 [SQL Server R Services 入门](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [R Services 安装问题疑难解答](http://msdn.microsoft.com/library/ce6b902b-a4fa-4b0a-ac0d-be47a59c2a78)  
  
  

