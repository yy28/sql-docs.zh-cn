---
title: "从命令行安装 Microsoft R Server | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 4
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 3
---
# 从命令行安装 Microsoft R Server
    
可通过使用 SQL Server 安装程序提供的脚本设施从命令行安装 Microsoft R Server。 

- **无人参与**安装要求指定安装实用程序的位置，并使用参数指示要安装的功能。 
- 对于**静默**安装，提供相同的参数并添加 **/q** 切换。 不提供提示，无需交互。 但是，如果遗漏了任何所需的参数，安装将失败。

有关详细信息，请参阅 [从命令提示符安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。

## <a name="perform-a-command-line-install-of-microsoft-r-server-standalone"></a>执行 Microsoft R Server（独立版）的命令行安装

 下面示例显示了使用 SQL Server 安装程序执行 Microsoft R Server 的命令行安装时使用的参数。


### <a name="example-of-unattended-installation-of-r-server-standalone"></a>R Server 独立版的无人参与安装示例

从提升的命令提示符运行以下命令，仅安装 Microsoft R Server（独立版）及其必备组件。 

```  
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS 
```  

若要查看进度和提示，删除 /q 参数。

请注意，所有以下参数均为必需参数：
  - **FEATURES = SQL_SHARED_MR** 仅获取 Microsoft R Server 组件，包括 Microsoft R Open 和任何必备组件。
  - **IACCEPTROPENLICENSETERMS** 指示已接受使用开放源 R 组件的许可证条款。
  - 运行安装向导需要 **IACCEPTSQLSERVERLICENSETERMS**。


### <a name="offline-installation"></a>脱机安装

如果在无法连接 Internet 的计算机上安装 Microsoft R Server（独立版），必须提前下载所需的 R 组件并将其复制到本地文件夹。 有关下载位置，请参阅[在没有 Internet 连接的情况下安装 R 组件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)。   


## <a name="advanced-installation-tips"></a>高级安装提示

安装程序完成后，可以查看 SQL Server 安装程序创建的配置文件以及安装程序操作的摘要。

SQL Server 的所有安装程序日志和摘要以及相关功能均默认在 `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log` 中创建。

为每个已安装功能创建单独的子文件夹。 对于 Microsoft R Server，请查找： 
- `RSetup.log`
- `Settings.xml`
- `Summmary<instance_GUID>.txt`

若要使用相同参数设置 Microsoft R Server 的其他实例，也可重新使用安装过程中创建的配置文件。 请参阅 [使用配置文件安装 SQL Server](https://msdn.microsoft.com/library/dd239405.aspx)，了解相关详细信息



### <a name="customizing-your-r-environment"></a>自定义 R 环境

安装完成后，可以安装其他 R 包。 有关详细信息，请参阅[安装和管理 R 包](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)。

> [!IMPORTANT]
> 如果要在 SQL Server 上运行 R 代码，请确保在运行 Microsoft R Server 的客户端计算机和运行 R 服务的 SQL Server 实例上安装相同的包。 



## <a name="see-also"></a>另请参阅  

[Microsoft R Server](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)
  