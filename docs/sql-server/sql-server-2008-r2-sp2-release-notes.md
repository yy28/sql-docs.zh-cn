---
title: "SQL Server 2008 R2 SP2 发行说明 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server 2008 R2 SP2
- Release Notes, SQL Server 2008 R2 SP2
ms.assetid: e2bd3de7-674c-4ea7-8d53-bb40bba86fae
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 978e780dd19e34c27ceef49ff8388f6ae1f155ed
ms.openlocfilehash: 25aba71ea2c8b7fc8b0944ad5731e6edcb161c37
ms.contentlocale: zh-cn
ms.lasthandoff: 09/02/2017

---
# <a name="sql-server-2008-r2-sp2-release-notes"></a>SQL Server 2008 R2 SP2 Release Notes
本发行说明文档介绍了在安装 Microsoft SQL Server 2008 R2 Service Pack 2 或者解决其相关问题之前应该了解的一些已知问题。 本发行说明文档适用于 SQL Server 2008 R2 SP2 的所有版本且只以联机形式提供。 文本档定期更新。  
  
## <a name="10-whats-new-in-service-pack-2"></a>1.0 Service Pack 2 中的新增功能  
添加了动态管理视图 (DMV) **sys.dm_db_stats_properties**。 您可以使用此 DMV 为当前数据库中指定的表或索引视图返回统计信息属性。 例如，此 DMV 可返回取样的行数和直方图梯级数。  
  
## <a name="20-before-you-install"></a>2.0 安装前  
有关如何安装 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 更新的信息，请参阅 [SQL Server 2008 R2 服务文档](http://msdn.microsoft.com/library/dd638062(SQL.105).aspx)(#sql-server-2008-r2-服务文档)。  
  
有关如何安装和开始使用 SQL Server 2008 R2 的一般信息，请参阅 SQL Server 2008 R2 自述文件。 安装介质中提供了自述文档。 您还可以在 [SQL Server 联机丛书](http://msdn.microsoft.com/library/ms130214.aspx) 中以及 [SQL Server 论坛](http://social.msdn.microsoft.com/Forums/category/sqlserver/)上找到更多的信息。  
  
### <a name="21-choose-the-correct-file-to-download-and-install"></a>2.1 正确选择要下载及安装的文件  
请使用下表来确定要下载和安装的文件。 安装 Service Pack 之前请验证您的系统是符合要求的。 表中链接的下载页上提供了系统要求。  
  
|如果您目前已经安装的版本是...|而您需要...|请下载和安装...|  
|-------------------------------------------|----------------------|---------------------------|  
|SQL Server 2008 R2 或 SQL Server 2008 R2 SP1 的任何版本的 32 位版|升级到 SQL Server 2008 R2 SP2 的 32 位版|SQLServer2008R2SP2-KB2630458-x86-ENU（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=251790)(#此处)）|  
|SQL Server 2008 R2 RTM Express 或 SQL Server 2008 R2 SP1 Express 的 32 位版|升级到 SQL Server 2008 R2 SP2 的 32 位版|SQLServer2008R2SP2-KB2630458-x86-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=251790)(#此处)）|  
|仅 SQL Server 2008 R2 或 SQL Server 2008 R2 SP1 的客户端和可管理性工具（包括 SQL Server 2008 R2 Management Studio）的 32 位版|将客户端和可管理性工具升级到 SQL Server 2008 R2 SP2 的 32 位版|SQLServer2008R2SP2-KB2630458-x86-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=251790)(#此处)）|  
|SQL Server 2008 R2 Management Studio Express 或 SQL Server 2008 R2 SP1 Management Studio Express 的 32 位版|升级到 SQL Server 2008 R2 SP2 Management Studio Express 的 32 位版|SQLManagementStudio_x86_ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=251791)(#此处)）|  
|SQL Server 2008 R2 或 SQL Server 2008 R2 SP1 的任何版本的 32 位版 **和** 客户端和可管理性工具（包括 SQL Server 2008 R2 RTM Management Studio）的 32 位版|将所有产品都升级到 SQL Server 2008 R2 SP2 的 32 位版|SQLServer2008R2SP2-KB2630458-x86-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=251790)(#此处)）|  
|[Microsoft SQL Server 2008 R2 RTM 功能包](http://www.microsoft.com/download/en/details.aspx?id=16978)(#microsoft-sql-server-2008-r2-rtm-功能包) 中一种或多种工具的 32 位版|将工具升级到 Microsoft SQL Server 2008 R2 SP2 功能包的 32 位版|[Microsoft SQL Server 2008 R2 SP2 功能包](http://go.microsoft.com/fwlink/?LinkId=251792)中的一个或多个文件|  
|没有安装 SQL Server 2008 R2 的 32 位版|安装 Server 2008 R2（包括 SP2）|转到 [SQL Server 2008 R2 SP2 – Express Edition](http://go.microsoft.com/fwlink/?LinkId=251791) 并按说明操作。|  
|没有安装 SQL Server 2008 R2 Management Studio 的 32 位版|安装 SQL Server 2008 R2 Management Studio（包括 SP2）|SQLManagementStudio_x86_ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=251791) (#此处)），以安装免费的 SQL Server 2008 R2 SP2 Management Studio Express Edition。|  
|SQL Server 2008 R2 或 SQL Server 2008 R2 SP1 的任何版本的 64 位版|升级到 SQL Server 2008 R2 SP2 的 64 位版|SQLServer2008R2SP2-KB2630458-x64-ENU or SQLServer2008R2SP2-KB2630455-IA64-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=251790)(#此处)）|  
|SQL Server 2008 R2 RTM Express 或 SQL Server 2008 R2 SP1 Express 的 64 位版|升级到 SQL Server 2008 R2 SP2 的 64 位版|SQLServer2008R2SP2-KB2630458-x64-ENU.exe 或 SQLServer2008R2SP2-KB2630455-IA64-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=251790)(#此处)）|  
|仅 SQL Server 2008 R2 或 SQL Server 2008 R2 SP1 的客户端和可管理性工具（包括 SQL Server 2008 R2 Management Studio）的 64 位版|将客户端和可管理性工具升级到 SQL Server 2008 R2 SP2 的 64 位版|SQLServer2008R2SP2-KB2630458-x64-ENU.exe 或 SQLServer2008R2SP2-KB2630455-IA64-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=251790)(#此处)）|  
|SQL Server 2008 R2 Management Studio Express 或 SQL Server 2008 R2 SP1 Management Studio Express 的 64 位版|升级到 SQL Server 2008 R2 SP2 Management Studio Express 的 64 位版|SQLManagementStudio_x64_ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=251791)(#此处)）|  
|SQL Server 2008 R2 或 SQL Server 2008 R2 SP1 的任何版本的 64 位版 **和** 客户端和可管理性工具（包括 SQL Server 2008 R2 RTM Management Studio）的 64 位版|将所有产品都升级到 SQL Server 2008 R2 SP2 的 64 位版|SQLServer2008R2SP2-KB2630458-x64-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=251790)(#此处)）|  
|[Microsoft SQL Server 2008 R2 RTM 功能包](http://www.microsoft.com/download/en/details.aspx?id=16978)(#microsoft-sql-server-2008-r2-rtm-功能包) 中一种或多种工具的 64 位版|将工具升级到 Microsoft SQL Server 2008 R2 SP2 功能包的 64 位版|[Microsoft SQL Server 2008 R2 SP2 功能包](http://go.microsoft.com/fwlink/?LinkId=251792)中的一个或多个文件|  
|没有安装 SQL Server 2008 R2 的 64 位版|安装 Server 2008 R2（包括 SP2）|转到 [SQL Server 2008 R2 SP2 – Express Edition](http://go.microsoft.com/fwlink/?LinkId=251791) 并按说明操作。|  
|没有安装 SQL Server 2008 R2 Management Studio 的 64 位版|安装 SQL Server 2008 R2 Management Studio（包括 SP2）|SQLManagementStudio_x64_ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=251791) (#此处)），以安装免费的 SQL Server 2008 R2 SP2 Management Studio Express Edition。|  
  
### <a name="22-setup-might-fail-if-sqagtresdll-is-locked-by-another-process"></a>2.2 如果另一进程锁定了 SQAGTRES.dll 可能会导致安装程序失败  
**问题**：SQL Server 安装程序操作可能会失败并出现如下错误： `Upgrading of cluster resource C:\Program Files\Microsoft SQL Server\MSSQL10_50.<Instance name>\MSSQL\Binn\SQAGTRES.DLL on machine <Computer name> failed with Win32Exception. Please look at inner exception for details.` 。根本原因是另一个进程锁定了 C:\Windows\system32\SQAGTRES.DLL 而安装程序无法更新它。  
  
**变通方法**：将 C:\Windows\system32\SQAGTRES.DLL 重命名为一个 C:\Windows\system32\SQAGTRES_old.DLL 这样的临时名称，然后选择安装程序错误信息上的“重试”选项。 这样，安装程序就可以继续运行了。 重新启动之后，您可以删除临时文件 C:\Windows\system32\SQAGTRES_old.DLL。  
  
## <a name="30-known-issues-fixed-in-this-service-pack"></a>3.0 此 Service Pack 中已修复的已知问题  
有关此 Service Pack 中已修复的 Bug 和已知问题的完整列表，请参阅此 [主知识库文章](http://support.microsoft.com/kb/2630455)。  
  
## <a name="see-also"></a>另请参阅  
[如何确定 SQL Server 的版本和版本类别](http://support.microsoft.com/kb/321185)  
  

