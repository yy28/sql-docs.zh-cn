---
title: 备份、 还原和移动 SSIS 目录 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: bf806aef-8556-48ab-aed5-e95de9a2204e
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2c2873a6864e3ac5d55f180bfc2555d8cb471620
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354482"
---
# <a name="backup-restore-and-move-the-ssis-catalog"></a>备份、还原和移动 SSIS 目录
  [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 包含 SSISDB 数据库。 查询 SSISDB 数据库中的视图可以检查 **SSISDB** 目录中存储的对象、设置和操作数据。 本主题说明如何备份和还原该数据库。  
  
 SSISDB 目录存储部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器的包。 有关该目录的详细信息，请参阅 [SSIS 目录](catalog/ssis-catalog.md)。  
  
##  <a name="backup"></a> 备份 SSIS 数据库  
  
1.  打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 并连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例。  
  
2.  使用 BACKUP MASTER KEY Transact-SQL 语句备份 SSISDB 数据库的主密钥。 该密钥存储在您指定的文件中。 使用密码加密该文件中的主密钥。  
  
     有关语句的详细信息，请参阅 [BACKUP MASTER KEY (Transact-SQL)](/sql/t-sql/statements/backup-master-key-transact-sql)。  
  
     在下面的示例中，将主密钥导出到 `c:\temp directory\RCTestInstKey` 文件。 使用 `LS2Setup!` 密码加密主密钥。  
  
    ```  
    backup master key to file = 'c:\temp\RCTestInstKey'  
           encryption by password = 'LS2Setup!'  
  
    ```  
  
3.  在 **中使用** “备份数据库” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]对话框备份 SSISDB 数据库。 有关详细信息，请参阅[如何备份数据库 (SQL Server Management Studio)](https://go.microsoft.com/fwlink/?LinkId=231812)。  
  
4.  通过执行以下操作，生成 ##MS_SSISServerCleanupJobLogin## 的 CREATE LOGIN 脚本。 有关详细信息，请参阅 [CREATE LOGIN (Transact-SQL)](/sql/t-sql/statements/create-login-transact-sql)。  
  
    1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的对象资源管理器中，展开 **“安全性”** 节点，然后展开 **“登录名”** 节点。  
  
    2.  右键单击 **##MS_SSISServerCleanupJobLogin##**，然后依次单击“编写登录脚本为” > “CREATE 到” > “新查询编辑器窗口”。  
  
5.  如果要将 SSISDB 数据库还原到从未创建 SSISDB 目录的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，请执行以下操作生成 sp_ssis_startup 的 CREATE PROCEDURE 脚本。 有关详细信息，请参阅 [CREATE PROCEDURE (Transact-SQL)](/sql/t-sql/statements/create-procedure-transact-sql)。  
  
    1.  在对象资源管理器中，展开“数据库”节点，然后展开“主” > “可编程性” > “存储过程”节点。  
  
    2.  右键单击 **dbo.sp_ssis_startup**，然后依次单击“编写存储过程脚本为” > “CREATE 到” > “新查询编辑器窗口”。  
  
6.  确认 SQL Server 代理已启动  
  
7.  如果要将 SSISDB 数据库还原到从不创建 SSISDB 目录的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，请执行以下操作生成 SSIS 服务器维护作业的脚本。 创建 SSISDB 目录时自动在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理中创建该脚本。 该作业帮助清除保留期窗口之外的操作日志并删除较旧版本的项目。  
  
    1.  在对象资源管理器中，展开 **“SQL Server 代理”** 节点，然后展开 **“作业”** 节点。  
  
    2.  右键单击“SSIS 服务器维护作业”，然后依次单击“编写作业脚本为” > “CREATE 到” > “新查询编辑器窗口”。  
  
### <a name="to-restore-the-ssis-database"></a>还原 SSIS 数据库  
  
1.  如果要将 SSISDB 数据库还原到从不创建 SSISDB 目录的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，请通过运行 sp_configure 存储过程来启用公共语言运行时 (clr)。 有关详细信息，请参阅 [sp_configure (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 和 [clr enabled 选项](https://go.microsoft.com/fwlink/?LinkId=231855)。  
  
    ```  
    use master   
           sp_configure 'clr enabled', 1  
           reconfigure  
  
    ```  
  
2.  如果要将 SSISDB 数据库还原到从不创建 SSISDB 目录的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，请创建非对称密钥和对应非对称密钥的登录名并将 UNSAFE 权限授予该登录名。  
  
    ```  
    Create Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey  
           FROM Executable File = 'C:\Program Files\Microsoft SQL Server\110\DTS\Binn\Microsoft.SqlServer.IntegrationServices.Server.dll'  
  
    ```  
  
     [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] CLR 存储过程要求将 UNSAFE 权限授予该登录名，因为该登录名需要对受限制资源（如 Microsoft Win32 API）的更高访问权限。 有关 UNSAFE 代码权限的详细信息，请参阅 [Creating an Assembly](../relational-databases/clr-integration/assemblies/creating-an-assembly.md)。  
  
    ```  
    Create Login MS_SQLEnableSystemAssemblyLoadingUser  
           FROM Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey   
  
           Grant unsafe Assembly to MS_SQLEnableSystemAssemblyLoadingUser  
  
    ```  
  
3.  在 **中使用** “还原数据库” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]对话框从备份中还原 SSISDB 数据库。 有关详细信息，请参阅以下主题。  
  
    -   [还原数据库（“常规”页）](general-page-of-integration-services-designers-options.md)  
  
    -   [还原数据库（“文件”页）](../relational-databases/backup-restore/restore-database-files-page.md)  
  
    -   [还原数据库（“选项”页）](../relational-databases/backup-restore/restore-database-options-page.md)  
  
4.  执行你在 [备份 SSIS 数据库](#backup) 中为 ##MS_SSISServerCleanupJobLogin##、sp_ssis_startup 和 SSIS 服务器维护作业创建的脚本。 确认 SQL Server 代理已启动。  
  
5.  运行以下语句以将 sp_ssis_startup 过程设置为自动执行。 有关详细信息，请参阅 [sp_procoption (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql)。  
  
    ```  
    EXEC sp_procoption N'sp_ssis_startup','startup','on'  
    ```  
  
6.  通过在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中使用“登录属性”对话框，将 SSISDB 用户 ##MS_SSISServerCleanupJobUser##（SSISDB 数据库）映射到 ##MS_SSISServerCleanupJobLogin##。  
  
7.  使用下列方法之一还原主密钥。 有关加密的详细信息，请参阅 [Encryption Hierarchy](../relational-databases/security/encryption/encryption-hierarchy.md)。  
  
    -   **方法 1**  
  
         如果已备份数据库主密钥且具有用于加密主密钥的密码，则使用此方法。  
  
        ```  
               Restore master key from file = 'c:\temp\RCTestInstKey'  
               Decryption by password = 'LS2Setup!' -- 'Password used to encrypt the master key during SSISDB backup'  
               Encryption by password = 'LS3Setup!' -- 'New Password'  
               Force  
  
        ```  
  
        > [!NOTE]  
        >  确认 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务帐户有权读取备份密钥文件。  
  
        > [!NOTE]  
        >  如果服务主密钥尚未加密数据库主密钥，将看到 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中显示的以下警告消息。 忽略警告消息。  
        >   
        >  **无法解密当前主密钥。此错误已被忽略，因为指定了 FORCE 选项。**  
        >   
        >  FORCE 参数指定即使当前数据库主密钥未打开，也应继续执行还原过程。 对于 SSISDB 目录，由于在您正在其中还原数据库的实例上未打开数据库主密钥，您将看到此消息。  
  
    -   **方法 2**  
  
         如果您具有用于创建 SSISDB 的原始密码，则使用此方法。  
  
        ```  
        open master key decryption by password = 'LS1Setup!' --'Password used when creating SSISDB'  
               Alter Master Key Add encryption by Service Master Key  
        ```  
  
8.  通过运行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] catalog.check_schema_version [，确定 SSISDB 目录架构与](/sql/integration-services/system-stored-procedures/catalog-check-schema-version)二进制文件（ISServerExec 和 SQLCLR 程序集）是否兼容。  
  
9. 若要确认 SSISDB 数据库已成功还原，请针对 SSISDB 目录执行操作，如运行部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器的包。 有关详细信息，请参阅 [使用 SQL Server Management Studio 在 SSIS 服务器上运行包](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)。  
  
### <a name="to-move-the-ssis-database"></a>移动 SSIS 数据库  
  
-   按移动用户数据库的说明操作。 有关详细信息，请参阅 [Move User Databases](../relational-databases/databases/move-user-databases.md)。  
  
     确保您备份 SSISDB 数据库的主密钥并保护备份文件。 有关详细信息，请参阅 [备份 SSIS 数据库](#backup)。  
  
     确保在尚未创建 SSISDB 目录的新 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例中创建 Integration Services (SSIS) 相关对象。  
  
  
