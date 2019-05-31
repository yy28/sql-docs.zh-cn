---
title: ADO.NET 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetconnection.f1
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bee4d3ea71aaeacf682a6e90fad91786fa7a0c9c
ms.sourcegitcommit: e92ce0f59345fe61c0dd3bfe495ef4b1de469d4b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2019
ms.locfileid: "66221176"
---
# <a name="adonet-connection-manager"></a>ADO.NET 连接管理器

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器使包能够使用 .NET 访问接口访问数据源。 此连接管理器通常用于访问 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]等数据源，也用于访问在用 C# 等语言以托管代码编写的自定义任务中通过 OLE DB 和 XML 公开的数据源。  
  
 将 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器添加到包时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建在运行时作为 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接进行解析的连接管理器，同时还会设置该连接管理器的属性，并将该连接管理器添加到包的 **Connections** 集合。  
  
 该连接管理器的 **ConnectionManagerType** 属性设置为 **ADO.NET**。 **ConnectionManagerType** 的值受到限定，以包含连接管理器所使用的 .NET 访问接口的名称。  
  
## <a name="adonet-connection-manager-troubleshooting"></a>ADO.NET 连接管理器故障排除  
 可以记录 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器对外部数据访问接口所做的调用。 使用此日志记录功能，可以对 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器与外部数据源的连接进行故障排除。 若要记录 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器在读取数据时，某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期数据类型的数据将生成下表中显示的结果。  
  
|SQL Server 数据类型|结果|  
|--------------------------|------------|  
|**time**、 **datetimeoffset**|除非包使用参数化 SQL 命令，否则，包将失败。 若要使用参数化 SQL 命令，请在包中使用执行 SQL 任务。 有关详细信息，请参阅 [执行 SQL 任务](../../integration-services/control-flow/execute-sql-task.md) 和 [执行 SQL 任务中的参数和返回代码](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)。|  
|**datetime2**|[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器截断毫秒值。|  
  
> [!NOTE]  
>  有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和它们如何映射到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型的详细信息，请参阅[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md) 和 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="adonet-connection-manager-configuration"></a>配置 ADO.NET 连接管理器  
 可以通过下列方式配置 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器：  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
-   提供配置为满足选定 .NET 访问接口的要求的特定连接字符串。  
  
-   包括要连接到的数据源的名称（取决于访问接口）。  
  
-   为选定的访问接口提供相应的安全凭据。  
  
-   指示是否在运行时保留从连接管理器中创建的连接。  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器的许多配置选项取决于该连接管理器所使用的 .NET 访问接口。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题之一：  
  
-   [配置 ADO.NET 连接管理器](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
## <a name="configure-adonet-connection-manager"></a>配置 ADO.NET 连接管理器
  可以使用 **“配置 ADO.NET 连接管理器”** 对话框，添加与可使用 .NET Framework 数据访问接口（例如，SqlClient 访问接口）访问的数据源之间的连接。 连接管理器可使用现有连接，或者您也可以创建一个新的连接。  
  
 若要了解有关 ADO.NET 连接管理器的详细信息，请参阅 [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)。  
  
### <a name="options"></a>选项  
 **数据连接**  
 从列表中选择一个现有的 ADO.NET 数据连接。  
  
 **数据连接属性**  
 查看所选 ADO.NET 数据连接的属性和值。  
  
 **新建**  
 通过使用“连接管理器”对话框创建 ADO.NET 数据连接。   
  
 **删除**  
 选择某个连接，然后可以使用“删除”按钮将其删除。   
  
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

1. **授予数据工厂托管标识所需的权限**。 对要复制数据的数据库运行以下 T-SQL：

    ```sql
    CREATE USER [{the managed identity name}] FOR LOGIN [{the managed identity name}] WITH DEFAULT_SCHEMA = dbo
    ALTER ROLE db_owner ADD MEMBER [{the managed identity name}]
    ```

最后，为 ADO.NET 连接管理器“配置托管标识”  。 完成此操作的方法有两种。
    
1. 在设计时进行配置。 在 SSIS 设计器中，右键单击 ADO.NET 连接管理器，然后单击“属性”以打开“属性窗口”   。 将属性“ConnectUsingManagedIdentity”更新为“True”   。
    > [!NOTE]
    >  当前在 SSIS 设计器或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 中运行 SSIS 包时，连接管理器属性“ConnectUsingManagedIdentity”不会生效（表示托管标识身份验证不起作用）  。
    
1. 在运行时进行配置。 通过 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) 或 [Azure 数据工厂执行 SQL 包活动执行包活动](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)时，找到 ADO.NET 连接管理器并将其属性“ConnectUsingManagedIdentity”更新为“True”   。
    > [!NOTE]
    >  在 Azure-SSIS 集成运行时中，当使用托管标识身份验证来建立数据库连接时，ADO.NET 连接管理器上预配的所有其他身份验证方法（例如，集成身份验证、密码）将被“重写”  。

> [!NOTE]
>  要在现有软件包上配置托管标识身份验证，请务必至少使用[最新 SSIS 设计器](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)重新生成一次 SSIS 项目，然后将该 SSIS 项目重新部署到 Azure-SSIS 集成运行时，以便新的连接管理器属性“ConnectUsingManagedIdentity”能自动添加到 SSIS 项目中的所有 ADO.NET 连接管理器  。

## <a name="see-also"></a>另请参阅  
 [Integration Services (SSIS) 连接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
