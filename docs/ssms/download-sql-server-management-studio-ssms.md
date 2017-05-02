---
title: "下载 SQL Server Management Studio (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 04/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "安装 SSMS，下载 SSMS，最新的 SSMS"
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- "SQL Management Studio 安装"
- "下载 SQL Management Studio"
- MS SQL Management Studio
- "安装 SQL Management Studio"
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
caps.latest.revision: 145
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cc827737cec19c11d2102f968dc2b8bc638bda86
ms.lasthandoff: 04/11/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>下载 SQL Server Management Studio (SSMS)
SQL Server Management Studio (SSMS) 是一个集成环境，用于访问、配置、控制、管理和开发 SQL Server 的所有组件。 SSMS 将大量图形工具与丰富的脚本编辑器相结合，使各种技术水平的开发人员和管理员都可以访问 SQL Server。 此版本改进了与以前版本的 SQL Server 的兼容性、具有独立 Web 安装程序以及新版本可用时 SSMS 内部的 Toast 通知。  

    
| ![下载](../ssdt/media/download.png) 下载 SQL Server Management Studio (SSMS)  |  |
|:---|:---|
|**[下载 SQL Server Management Studio (16.5.3)](https://go.microsoft.com/fwlink/?LinkID=840946)**|用于生产的当前版本。|
|**[下载 SQL Server Management Studio - 候选发布 (17.0 RC3)](../ssms/sql-server-management-studio-ssms-release-candidate.md)**|支持 SQL Server vNext CTP1.3，并可与 16.x 并行使用，但不建议用于生产。| 


> [!NOTE]
> SSMS 版本目前以数字命名，不按月份命名。 SSMS 是免费的！ 它无需许可证即可安装和使用。  


## <a name="sql-server-management-studio"></a>SQL Server Management Studio   
**版本信息**  
  
版本号：16.5.3  
此版本的内部版本号为：13.0.16106.4
  
**支持的 SQL Server 版本**  
  
* 此版本的 SSMS 适用于所有 [受支持版本的 SQL Server (SQL Server 2008 - SQL Server 2016)](https://support.microsoft.com/en-us/lifecycle?C2=1044) ，并且在最大程度上支持与 Azure SQL 数据库和 Azure SQL 数据仓库中的最新云功能配合使用。  
* 没有显式阻止 SQL Server 2000 或 SQL Server 2005，但某些功能可能无法正常工作。  
* 此外，可在安装 SSMS 2014 及更早版本时并行安装一个 SSMS 16.x 版本或 SSMS 2016。 
  
**支持的操作系统**  
  
此版本的 SSMS 在与最新可用的 Service Pack 一起使用时支持以下平台：   
 Windows 10、Windows 8、Windows 8.1、Windows 7 (SP1)、Windows Server 2012（64 位）、Windows Server 2012 R2（64 位）、Windows Server 2008 R2（64 位）  
   
 **支持的语言**  
> [!NOTE]  
> 如果安装在以下平台中，非英语本地化版本的 SSMS 需要 [KB 2862966 安全更新程序包](https://support.microsoft.com/en-us/kb/2862966) ：Windows 8、Windows 7、Windows Server 2012 和 Windows Server 2008 R2。 
  
 此版本的 SSMS 可以安装在以下语言中：  
[中文（中国大陆）](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804) | [中文（中国台湾）](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404) | [英语（美国）](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409) | [法语](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c)  
[德语](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407) | [意大利语](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410) | [日语](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411) | [朝鲜语](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412) | [葡萄牙语（巴西）](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416) | [俄语](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419) | [西班牙语](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)  

 
## <a name="changelog"></a>更改日志  

16.5.3

此版本已解决以下问题：

* 解决了 SSMS 16.5.2 中引入的问题，即当表具有多个稀疏列时，导致“表”节点扩展。

* 用户可以部署包含 OData 连接管理器的 SSIS 包，这些包连接到 SSIS 目录的 Microsoft Dynamics AX / CRM Online 资源。 有关详细信息，请参阅 [OData 连接管理器](https://msdn.microsoft.com/library/dn584133.aspx)。

* 为现有表配置“始终加密”功能失败，在不相关的对象上出错。 [连接 ID 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* 为现有数据库配置“始终加密”功能时，多个架构无法正常运行。 [连接 ID 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* 由于数据库包含引用系统视图的视图，“始终加密、已加密列”向导失败。 [连接 ID 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* 使用“始终加密”功能进行加密时，错误处理加密后刷新模块出现错误。

* “打开最近的文件”菜单不显示最近保存的文件。** [连接 ID 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* 右键单击表的索引（通过远程 (Internet) 连接）时，SSMS 运行缓慢。 [连接 ID 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* 解决了 SQL 设计器滚动条的问题。 [连接 ID 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* 表的上下文菜单暂时挂起 
 
* SSMS 偶尔在活动监视器中引发异常和崩溃。 [连接 ID 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016 崩溃，显示错误“由于在 IP 71AF8579 (71AE0000) 的 .NET 运行时出现内部错误，进程终止，退出代码 80131506”





有关功能的完整列表，请参阅    
                [SQL Server Management Studio (SSMS) - 更改日志](../ssms/sql-server-management-studio-changelog-ssms.md)  
  
若要查看已知问题和解决方法的列表，请参阅   
                [SQL Server Management Studio - 发行说明](../ssms/sql-server-management-studio-release-notes.md)  
  
有关用户数据收集的信息，请参阅   
                [SQL Server 隐私声明](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx)。  
  
## <a name="previous-releases"></a>以前的版本  
[旧版 SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  
  
## <a name="feedback"></a>反馈  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 客户端工具论坛](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 中提出问题或建议](https://connect.microsoft.com/SQLServer/Feedback)。  
  
## <a name="see-also"></a>另请参阅  
[教程：SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[SQL Server Management Studio 文档](https://msdn.microsoft.com/library/hh213248(v=sql.130).aspx)  
[Microsoft SQL Server](https://msdn.microsoft.com/library/bb545450.aspx)  
[其他更新程序和 Service Pack](https://technet.microsoft.com/sqlserver/ff803383.aspx)  
[下载 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  



