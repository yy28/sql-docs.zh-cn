---
title: Ssms 实用工具 | Microsoft Docs
ms.custom: ''
ms.date: 12/08/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], opening
- command prompt utilities [SQL Server], sqlwb
- sqlwb utility
- Management Studio command line
- opening SQL Server Management Studio
ms.assetid: aafda520-9e2a-4e1e-b936-1b165f1684e8
caps.latest.revision: 50
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c8c64df36bef9012e91d444f9f5326a4e746b543
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926468"
---
# <a name="ssms-utility"></a>Ssms 实用工具
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Ssms 实用工具打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 如果指定， **Ssms** 还可以与服务器建立连接并打开查询、脚本、文件、项目和解决方案。  
  
 可以指定包含查询、项目或解决方案的文件。 如果提供了连接信息并且文件类型与服务器类型关联，则包含查询的文件将自动连接到该服务器。 例如，sql 文件将在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中打开一个 SQL 查询编辑器窗口，.mdx 文件将在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中打开一个 MDX 查询编辑器窗口。 **“SQL Server 解决方案和项目”** 将在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中打开。  
  
> [!NOTE]  
>  **Ssms** 实用工具不能运行查询。 若要从命令行运行查询，请使用 **sqlcmd** 实用工具。  
  
## <a name="syntax"></a>语法  
  
```  
  
Ssms  
    [scriptfile] [projectfile] [solutionfile]  
    [-S servername] [-d databasename] [-G] [-U username] [-P password]   
    [-E] [-nosplash] [-log [filename]?] [-?]  
```  
  
## <a name="arguments"></a>参数  
 *scriptfile*  
 指定一个或多个要打开的脚本文件。 该参数必须包含文件的完整路径。  
  
 *projectfile*  
 指定要打开的脚本项目。 该参数必须包含脚本项目文件的完整路径。  
  
 *solutionfile*  
 指定要打开的解决方案。 该参数必须包含解决方案文件的完整路径。  
  
 [**-S** *servername*]  
  服务器名称  
  
 [**-d** *databasename*]  
  数据库名称  

 [-G] 使用 Active Directory 身份验证进行连接。 连接类型的确定取决于是否包含 -P 和/或 -U。
 - 如果不包含 -U 和 -P，则使用“Active Directory - 集成”，且不会出现对话框。
 - 如果 -U 和 -P 都包含在内，则使用“Active Directory - 密码”。 不建议使用此选项，因为你必须在命令行上指定明文密码，而这种操作是应当避免的。
 - 如果包含 -U，但缺失 -P，将弹出身份验证对话框，但所有登录尝试将都失败。 

  请注意，当前不支持“Active Directory - 通用且具有 MFA 支持”。 
  
[**-U** *username*]  
 使用“SQL 身份验证”或“Active Directory - 密码”进行连接时的用户名称  
  
[**-P** *password*]  
 使用“SQL 身份验证”或“Active Directory - 密码”进行连接时的密码
  
[**-E**]  
 使用 Windows 身份验证进行连接  
  
[**-nosplash**]  
 阻止 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 在打开时显示初始屏幕。 在带宽有限的情况下，通过终端服务连接到运行 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的计算机上时，使用此选项。 该参数不区分大小写，并且可放在其他参数前后  
  
[**-log***[filename]?*]  
 将 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 活动记录到指定的文件中以便进行故障排除  
  
[**-?**]  
 显示命令行帮助  
  
## <a name="remarks"></a>Remarks  
 上述所有开关都是可选的，并用空格分隔，但文件用逗号分隔。 如果不指定任何开关，则 **Ssms** 将按照“工具”菜单的“选项”设置中指定的方式打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 例如，如果“环境/常规”页的“启动时”选项指定了“打开新查询窗口”，**Ssms** 则会在打开时显示一个空白的查询编辑器。  
  
 **-log** 开关必须出现在命令行的末尾，位于所有其他开关的后面。 文件名参数是可选的。 如果指定了一个文件名，并且该文件不存在，则创建该文件。 如果无法创建该文件 – 例如，由于没有足够的写访问权限，日志将改为写入非本地化的 APPDATA 位置（见下文）。 如果未指定该文件名参数，则两个文件将写入当前用户的非本地化的应用程序数据文件夹。 SQL Server 的非本地化的应用程序数据文件夹可以从 APPDATA 环境变量中找到。 例如，对于 SQL Server 2012，文件夹为 \<system drive>:\Users\\<username\>\AppData\Roaming\Microsoft\AppEnv\10.0\\。 默认情况下，这两个文件分别命名为 ActivityLog.xml 和 ActivityLog.xsl。 前者包含活动日志数据，后者是一种 XML 样式表，提供了更方便的方法来查看 XML 文件。 按照下列步骤操作，在默认 XML 查看器（如 Internet Explorer）中查看日志文件：依次单击“开始”和“运行...”，在提供的字段中键入“\<system drive>:\Users\\<username\>\AppData\Roaming\Microsoft\AppEnv\10.0\ActivityLog.xml”，再按 Enter。  
  
 如果提供了连接信息并且文件类型与服务器类型关联，则包含查询的文件将立即连接到该服务器。 例如，sql 文件将在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中打开一个 SQL 查询编辑器窗口，.mdx 文件将在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中打开一个 MDX 查询编辑器窗口。 **“SQL Server 解决方案和项目”** 将在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中打开。  
  
 下表列出了与服务器类型相对应的文件扩展名。  
  
|服务器类型|扩展名|  
|-----------------|---------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|.sql|  
|SQL Server Analysis Services|.mdx<br /><br /> .xmla|  
  
## <a name="examples"></a>示例  
 以下脚本将在命令指示符下使用默认设置打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ：  
  
```  
Ssms  
  
```  
  
 以下脚本将在命令提示符下，使用“Active Directory - 集成”打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]：  
  
```  
Ssms.exe -S servername.database.windows.net -G
  
``` 


 以下脚本将在命令指示符下，使用 Windows 身份验证打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，其中代码编辑器设置为 `ACCTG and the database AdventureWorks2012,` ，并且不显示初始屏幕：  
  
```  
Ssms -E -S ACCTG -d AdventureWorks2012 -nosplash  
  
```  

 以下脚本将在命令指示符下打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，并打开 MonthEndQuery 脚本。  
  
```  
Ssms "C:\Documents and Settings\username\My Documents\SQL Server Management Studio Projects\FinanceScripts\FinanceScripts\MonthEndQuery.sql"  
  
```  
  
 以下脚本在命令指示符下打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，并打开名为 `developer`的计算机上的 NewReportsProject 项目：  
  
```  
Ssms "\\developer\fin\ReportProj\ReportProj\NewReportProj.ssmssqlproj"  
  
```  
  
 以下脚本在命令提示符下打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，并打开 MonthlyReports 解决方案：  
  
```  
Ssms "C:\solutionsfolder\ReportProj\MonthlyReports.ssmssln"  
  
```  
 



## <a name="see-also"></a>另请参阅  
 [使用 SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
  
  
