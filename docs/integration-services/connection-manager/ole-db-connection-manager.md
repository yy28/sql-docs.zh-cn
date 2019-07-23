---
title: OLE DB 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbconnection.f1
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 70e439dd6ed176fbb9c2d2fe666b314bd48f2f9c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904270"
---
# <a name="ole-db-connection-manager"></a>OLE DB 连接管理器

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  OLE DB 连接管理器使包能够用 OLE DB 访问接口连接到数据源。 例如，连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 OLE DB 连接管理器可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。    
    
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 OLEDB 提供程序不支持用于多子网故障转移群集的新连接字符串关键字 (MultiSubnetFailover=True)。 有关详细信息，请参阅 [SQL Server 发行说明](https://go.microsoft.com/fwlink/?LinkId=247824) 以及 www.mattmasson.com 上博客文章 [AlwaysOn 多子网故障转移和 SSIS](https://www.mattmasson.com/2012/03/alwayson-multi-subnet-failover-and-ssis/)。    
> 
> [!NOTE]
>  如果数据源是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007，则数据源需要不同于早期版本 Excel 或 Access 的数据访问接口。 有关详细信息，请参阅 [连接到 Excel 工作簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md) 和 [连接到 Access 数据库](../../integration-services/connection-manager/connect-to-an-access-database.md)。    
    
 有若干 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 任务和数据流组件使用 OLE DB 连接管理器。 例如，OLE DB 源和 OLE DB 目标使用这种连接管理器来提取和加载数据，而执行 SQL 任务可以使用这种连接管理器来连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库以运行查询。    
    
 OLE DB 连接管理器还用于在以使用 C++ 等语言的非托管代码编写的自定义任务中访问 OLE DB 数据源。    
    
 将 OLE DB 连接管理器添加到包时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时决定 OLE DB 连接的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到包上的“连接”  集合。    
    
 该连接管理器的 **ConnectionManagerType** 属性设置为 **OLEDB**。    
    
 可以按下列方式配置 OLE DB 连接管理器：    
    
-   提供配置为满足选定访问接口要求的特定连接字符串。    
    
-   包括要连接到的数据源的名称（取决于访问接口）。    
    
-   为选定的访问接口提供相应的安全凭据。    
    
-   指示是否在运行时保留从连接管理器中创建的连接。    
    
## <a name="logging"></a>日志记录    
 可以记录 OLE DB 连接管理器对外部数据访问接口所做的调用。 使用此日志记录功能，可以对 OLE DB 连接管理器与外部数据源的连接进行故障排除。 若要记录 OLE DB 连接管理器对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。    
    
## <a name="configuration-of-the-oledb-connection-manager"></a>OLEDB 连接管理器的配置    
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [配置 OLE DB 连接管理器](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)。 有关以编程方式配置连接管理器的信息，请参阅开发人员指南中针对 **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** 类的文档。    
    
## <a name="related-content"></a>相关内容    
    
-   social.technet.microsoft.com 上的 Wiki 文章 [SSIS 与 Oracle 连接器](https://go.microsoft.com/fwlink/?LinkId=220670) 。    
    
-   carlprothman.net 上的技术文章 [Connection Strings for OLE DB Providers](https://go.microsoft.com/fwlink/?LinkId=220744)（OLE DB 访问接口的连接字符串）。    
    
## <a name="configure-ole-db-connection-manager"></a>配置 OLE DB 连接管理器
  可以使用 **“配置 OLE DB 连接管理器”** 对话框添加数据源连接，添加的连接可以是新连接，也可以是现有连接的副本。  
  
> [!NOTE]  
>  如果数据源是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007，则数据源需要一个不同于早期版本 Excel 的连接管理器。 有关详细信息，请参阅 [连接到 Excel 工作簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)。  
>   
>  如果数据源是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007，则数据源需要一个不同于早期版本 Access 的 OLE DB 访问接口。 有关详细信息，请参阅 [连接到 Access 数据库](../../integration-services/connection-manager/connect-to-an-access-database.md)。  
  
 若要了解有关 OLE DB 连接管理器的详细信息，请参阅 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
### <a name="options"></a>选项  
 **数据连接**  
 从列表中选择现有的 OLE DB 数据连接。  
  
 **数据连接属性**  
 查看所选 OLE DB 数据连接的属性和值。  
  
 **新建**  
 使用“连接管理器”  对话框来创建 OLE DB 数据连接。  
  
 **删除**  
 选择一个数据连接，然后使用“删除”  按钮来删除该连接。  
  
### <a name="managed-identities-for-azure-resources-authentication"></a>Azure 资源身份验证的托管标识
在 [Azure 数据工厂中的 Azure-SSIS 集成运行时](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime)上运行 SSIS 包时，可以使用与数据工厂关联的[托管标识](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity)进行 Azure SQL 数据库（或托管实例）身份验证。 指定的工厂可以使用此标识访问数据库数据或从/向数据库复制数据。

要对 Azure SQL 数据库使用托管身份验证，请按照以下步骤配置数据库：

1. **在 Azure AD 中创建组。** 使托管标识成为该组的成员。
    
   1. [从 Azure 门户中查找数据工厂托管标识](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)。 转到数据工厂的“属性”  。 复制“托管标识对象 ID”  。
    
   1. 安装 [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2) 模块。 使用 `Connect-AzureAD` 命令登录。 运行以下命令以创建组并将托管标识添加为成员。
      ```powershell
      $Group = New-AzureADGroup -DisplayName "<your group name>" -MailEnabled $false -SecurityEnabled $true -MailNickName "NotSet"
      Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId "<your data factory managed identity object ID>"
      ```
    
1. 在 Azure 门户上为 Azure SQL 服务器[预配 Azure Active Directory 管理员](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)（如果尚未执行该操作）  。 Azure AD 管理员可以是 Azure AD 用户或 Azure AD 组。 如果为具有托管标识的组授予管理员角色，请跳过步骤 3 和 4。 管理员将拥有对数据库的完全访问权限。

1. 为 Azure AD 组[创建包含的数据库用户](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)  。 使用 SSMS 等工具连接到要从/向其复制数据的数据库，其 Azure Azure 标识至少具有 ALTER ANY USER 权限。 运行以下 T-SQL： 
    
    ```sql
    CREATE USER [your AAD group name] FROM EXTERNAL PROVIDER;
    ```

1. 授予 Azure AD 组所需的权限，就像通常为 SQL 用户和其他用户所做的那样  。 例如，运行以下代码：

    ```sql
    ALTER ROLE [role name] ADD MEMBER [your AAD group name];
    ```

要对 Azure SQL 数据库托管实例使用托管身份验证，请按照以下步骤配置数据库：
    
1. 在 Azure 门户上为托管实例[预配 Azure Active Directory 管理员](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-managed-instance)（如果尚未执行该操作）  。 Azure AD 管理员可以是 Azure AD 用户或 Azure AD 组。 如果为具有托管标识的组授予管理员角色，请跳过步骤 2-5。 管理员将拥有对数据库的完全访问权限。

1. [从 Azure 门户中查找数据工厂托管标识](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)  。 转到数据工厂的“属性”  。 复制“托管标识应用程序 ID”（非托管标识对象 ID）   。

1. **将数据工厂托管标识转换为二进制类型**。 使用 SSMS 等工具和 SQL/Active Directory 管理员帐户连接到托管实例中的“master”数据库  。 对“master”数据库运行以下 T-SQL，以获得二进制的托管标识应用程序 ID  ：
    
    ```sql
    DECLARE @applicationId uniqueidentifier = '{your managed identity application ID}'
    select CAST(@applicationId AS varbinary)
    ```

1. 在 Azure SQL 数据库托管实例中将数据工厂托管标识添加为用户  。 针对 master 数据库运行以下T-SQL  ：
    
    ```sql
    CREATE LOGIN [{a name for the managed identity}] FROM EXTERNAL PROVIDER with SID = {your managed identity application ID as binary}, TYPE = E
    ```

1. **向数据工厂托管标识授予所需的权限**。 对要从/向其复制数据的数据库运行以下 T-SQL：

    ```sql
    CREATE USER [{the managed identity name}] FOR LOGIN [{the managed identity name}] WITH DEFAULT_SCHEMA = dbo
    ALTER ROLE db_owner ADD MEMBER [{the managed identity name}]
    ```

然后为 OLE DB 连接管理器配置 OLE DB 提供程序  。 完成此操作的方法有两种。
    
1. 在设计时进行配置。 在 SSIS 设计器中，双击 OLE DB 连接管理器以打开“连接管理器”窗口  。 在“提供程序”下拉列表中，选择[适用于 SQL Server 的 Microsoft OLE DB 驱动程序](https://go.microsoft.com/fwlink/?linkid=871294)   。
    > [!NOTE]
    >  下拉列表中的其他提供程序可能不支持托管标识身份验证。
    
1. 在运行时进行配置。 通过 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) 或 [Azure 数据工厂执行 SSIS 包活动](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)执行包时，找到用于 OLE DB 连接管理器的连接管理器属性“ConnectionString”，将连接属性“Provider”更新为“MSOLEDBSQL”（即，Microsoft OLE DB Driver for SQL Server）    。
    ```vb
    Data Source=serverName;Initial Catalog=databaseName;Provider=MSOLEDBSQL;...
    ```

最后，为 OLE DB 连接管理器“配置托管标识身份验证”  。 完成此操作的方法有两种。
    
1. 在设计时进行配置。 在 SSIS 设计器中，右键单击 OLE DB 连接管理器，然后单击“属性”以打开“属性窗口”   。 将属性“ConnectUsingManagedIdentity”更新为“True”   。
    > [!NOTE]
    >  当前在 SSIS 设计器或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 中运行 SSIS 包时，连接管理器属性“ConnectUsingManagedIdentity”不会生效（表示托管标识身份验证不起作用）  。

1. 在运行时进行配置。 通过 SSMS 或执行 SQL 包活动执行包时，找到 OLE DB 连接管理器并将其属性“ConnectUsingManagedIdentity”更新为“True”   。
    > [!NOTE]
    >  在 Azure-SSIS 集成运行时中，当使用托管标识身份验证来建立数据库连接时，OLE DB 连接管理器上预配的所有其他身份验证方法（例如，集成安全性、密码）将被“重写”  。

> [!NOTE]
>  要在现有软件包上配置托管标识身份验证，请务必至少使用[最新 SSIS 设计器](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)重新生成一次 SSIS 项目，然后将该 SSIS 项目重新部署到 Azure-SSIS 集成运行时，以便新的连接管理器属性“ConnectUsingManagedIdentity”能自动添加到 SSIS 项目中的所有 OLE DB 连接管理器  。

## <a name="see-also"></a>另请参阅    
 [OLE DB 源](../../integration-services/data-flow/ole-db-source.md)     
 [OLE DB 目标](../../integration-services/data-flow/ole-db-destination.md)     
 [执行 SQL 任务](../../integration-services/control-flow/execute-sql-task.md)     
 [Integration Services (SSIS) 连接](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  
