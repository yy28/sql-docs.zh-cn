---
title: "创建 Analysis Services 作业步骤 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- job steps [Analysis Services]
ms.assetid: 03d4bb86-514b-4a55-97b9-c2c0fa08b428
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a1329ecb44429b9f353324c79e032d485f93a8dc
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="create-an-analysis-services-job-step"></a>Create an Analysis Services Job Step
本主题说明如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 中创建和定义通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 或 SQL Server 管理对象执行 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]Analysis Services 命令和查询的 [!INCLUDE[tsql](../../includes/tsql_md.md)] 代理作业步骤。  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要使用 Analysis Services 命令和/或查询创建 SQL Server 作业步骤，请使用：**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理对象](#SMO)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
  
-   如果作业步骤使用 Analysis Services 命令，则命令语句必须是 XML for Analysis Services **Execute** 方法。 该语句可以不包含完整的简单对象访问协议 (SOAP) 信封和 XML for Analysis **Discover** 方法。 虽然 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 支持完整的 SOAP 信封和 **Discover** 方法，但是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业步骤却不支持。 有关 XML for Analysis Services 的详细信息，请参阅 [XML for Analysis 概述 (XMLA)](http://msdn.microsoft.com/library/ms187190.aspx)。  
  
-   如果作业步骤使用 Analysis Services 查询，则查询语句必须是多维表达式 (MDX) 查询。 有关 MDX 的详细信息，请参阅 [MDX 语句基础知识 (MDX)](http://msdn.microsoft.com/en-us/a560383b-bb58-472e-95f5-65d03d8ea08b)。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
  
-   若要运行使用 Analysis Services 子系统的作业步骤，用户必须是 **sysadmin** 固定服务器角色的成员或有权访问为使用该子系统而定义的有效代理帐户。 此外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务帐户或代理必须是 Analysis Services 管理员或有效的 Windows 域帐户。  
  
-   只有 **sysadmin** 固定服务器角色的成员才可以将作业步骤输出写入到文件中。 如果运行作业步骤的用户是 **msdb** 数据库中 **SQLAgentUserRole** 数据库角色的成员，则输出只能写入表中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理会将作业步骤输出写入 **msdb** 数据库中的 **sysjobstepslog** 表。  
  
-   有关详细信息，请参阅 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>创建 Analysis Services 命令作业步骤  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  展开“SQL Server 代理”，创建一个新作业或右键单击一个现有作业，再单击“属性”。 有关创建作业的详细信息，请参阅[创建作业](../../ssms/agent/create-jobs.md)。  
  
3.  在 **“作业属性”** 对话框中，单击 **“步骤”** 页面，再单击 **“新建”**。  
  
4.  在 **“新建作业步骤”** 对话框中，键入作业 **“步骤名称”**。  
  
5.  在 **“类型”** 列表中，单击 **“SQL Server Analysis Services 命令”**。  
  
6.  在 **“运行身份”** 列表中，选择为使用 Analysis Services 命令子系统而定义的代理。 如果用户是 **sysadmin** 固定服务器角色的成员，还可以选择 **“SQL Agent 服务帐户”** 运行此作业步骤。  
  
7.  选择用于运行作业步骤的 **“服务器”** 或键入服务器名称。  
  
8.  在 **“命令”** 框中，键入要执行的语句，或者单击 **“打开”** 选择一个语句。  
  
9. 单击 **“高级”** 页可定义此作业步骤的选项，例如在作业步骤成功或失败时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理所应执行的操作、作业步骤的尝试次数以及用于写入作业步骤输出的位置。  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>创建 Analysis Services 查询作业步骤  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  展开“SQL Server 代理”，创建一个新作业或右键单击一个现有作业，再单击“属性”。 有关创建作业的详细信息，请参阅[创建作业](../../ssms/agent/create-jobs.md)。  
  
3.  在 **“作业属性”** 对话框中，单击 **“步骤”** 页，再单击 **“新建”**。  
  
4.  在 **“新建作业步骤”** 对话框中，键入作业的 **“步骤名称”**。  
  
5.  在 **“类型”** 列表中，单击 **“SQL Server Analysis Services 查询”**。  
  
6.  在 **“运行身份”** 列表中，选择为使用 Analysis Services 查询子系统而定义的代理。 如果用户是 **sysadmin** 固定服务器角色的成员，还可以选择 **“SQL Agent 服务帐户”** 运行此作业步骤。  
  
7.  选择用于运行作业步骤的 **“服务器”** 和 **“数据库”** ，或者键入服务器或数据库的名称。  
  
8.  在 **“命令”** 框中，键入要执行的语句，或者单击 **“打开”** 选择一个语句。  
  
9. 单击 **“高级”** 页可定义此作业步骤的选项，例如在作业步骤成功或失败时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理所应执行的操作、作业步骤的尝试次数以及用于写入作业步骤输出的位置。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>创建 Analysis Services 命令作业步骤  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- Creates a job step that uses XMLA to create a relational data source that
    -- references the AdventureWorks2012 Microsoft SQL Server database.  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name =
            N'Create a relational data source that references the AdventureWorks2012 Microsoft SQL Server database',  
        @subsystem = N'ANALYSISCOMMAND',  
        @command =
            N' <Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
        <ParentObject>  
            <DatabaseID>AdventureWorks2012</DatabaseID>  
        </ParentObject>  
        <ObjectDefinition>  
            <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:type="RelationalDataSource">  
                <ID>AdventureWorks2012</ID>  
                <Name>Adventure Works 2012</Name>  
                <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorks2012;Integrated Security=True</ConnectionString>  
                <ImpersonationInfo>  
                    <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
                </ImpersonationInfo>  
                <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
                <Timeout>PT0S</Timeout>  
            </DataSource>  
        </ObjectDefinition>  
    </Create>', ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755)。  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>创建 Analysis Services 查询作业步骤  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- Creates a job step that uses MDX to return data  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Returns the Internet sales amount by state',  
        @subsystem = N'ANALYSISQUERY',  
        @command = N' SELECT  
       [Measures].[Internet Sales Amount] ON COLUMNS,  
       [Customer].[State-Province].Members ON ROWS  
    FROM [AdventureWorks2012]',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755)。  
  
## <a name="SMO"></a>使用 SQL Server 管理对象  
**创建 PowerShell 脚本作业步骤**  
  
通过使用所选的编程语言（如 XMLA 或 MDX）来使用 **JobStep** 类。 有关详细信息，请参阅 [SQL Server 管理对象 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  

