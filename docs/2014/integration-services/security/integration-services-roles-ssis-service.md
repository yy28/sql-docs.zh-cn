---
title: Integration Services 角色（SSIS 服务）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], roles
- db_ssisoperator role
- db_ssisadmin role
- fixed database roles [Integration Services]
- packages [Integration Services], security
- roles [Integration Services]
- db_ssisltduser role
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9914bc878f1644ce6f8c8676e3b27178de99f5ea
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273524"
---
# <a name="integration-services-roles-ssis-service"></a>Integration Services 角色（SSIS 服务）
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括三个固定的数据库级别角色`db_ssisadmin`， **db_ssisltduser**，和**db_ssisoperator**，用于控制对包的访问。 仅在保存到包上实现角色`msdb`数据库中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]将角色分配给包。 角色分配保存到`msdb`数据库。  
  
## <a name="read-and-write-actions"></a>读取和写入操作  
 下表介绍了 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中 Windows 和固定数据库级角色的读写操作。  
  
|角色|读操作|写操作|  
|----------|-----------------|------------------|  
|`db_ssisadmin`<br /><br /> 或多个<br /><br /> `sysadmin`|枚举自己的包。<br /><br /> 枚举所有包。<br /><br /> 查看自己的包。<br /><br /> 查看所有包。<br /><br /> 执行自己的包。<br /><br /> 执行所有包。<br /><br /> 导出自己的包。<br /><br /> 导出所有包。<br /><br /> 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理中执行所有包。|导入包。<br /><br /> 删除自己的包。<br /><br /> 删除所有包。<br /><br /> 更改自己的包角色。<br /><br /> 更改所有包角色。<br /><br /> <br /><br /> **\*\* 重要\* \* ** db_ssisadmin 角色和 dc_admin 角色的成员可以将其特权提升为 sysadmin。 因为这些角色可以修改 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包，而 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的 sysadmin 安全上下文可以执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包，所以可以实现特权提升。 若要在运行维护计划、数据收集组和其他 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包时防止此权限提升，请将运行包的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业配置为使用具有有限权限的代理帐户，或只将 sysadmin 成员添加到 db_ssisadmin 和 dc_admin 角色。|  
|**db_ssisadmin**|枚举自己的包。<br /><br /> 枚举所有包。<br /><br /> 查看自己的包。<br /><br /> 执行自己的包。<br /><br /> 导出自己的包。|导入包。<br /><br /> 删除自己的包。<br /><br /> 更改自己的包角色。|  
|**db_ssisltduser**|枚举所有包。<br /><br /> 查看所有包。<br /><br /> 执行所有包。<br /><br /> 导出所有包。<br /><br /> 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理中执行所有包。|InclusionThresholdSetting|  
|**Windows 管理员**|查看所有正在运行的包的详细执行信息。|停止所有当前正在运行的包。|  
  
## <a name="sysssispackages-table"></a>Sysssispackages 表  
 **Sysssispackages**表中`msdb`包含的包保存到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅 [sysssispackages (Transact-SQL)](/sql/relational-databases/system-tables/sysssispackages-transact-sql)。  
  
 **sysssispackages** 表的列中包含关于分配给包的角色的信息。  
  
-   **readerrole** 列指定对包具有读访问权限的角色。  
  
-   **writerrole** 列指定对包具有写访问权限的角色。  
  
-   **ownersid** 列包含创建包的用户的唯一安全标识符。 此列定义包的所有者。  
  
## <a name="permissions"></a>权限  
 默认情况下的权限`db_ssisadmin`并**db_ssisoperator**固定的数据库级角色以及创建包的用户的唯一安全标识符适用于程序包和权限的读取器角色`db_ssisadmin`角色和创建包的用户的唯一安全标识符适用于写入者角色。 用户必须是属于`db_ssisadmin`， **db_ssisltduser**，或**db_ssisoperator**角色拥有对包的读取访问权限。 用户必须是属于`db_ssisadmin`角色才能拥有写访问权限。  
  
## <a name="access-to-packages"></a>对包的访问  
 固定数据库级角色可以与用户定义的角色结合使用。 用户定义的角色就是你在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中创建的、随后用来为包分配权限的角色。 若要访问包，用户必须是用户定义的角色和相关的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 固定数据库级角色的成员。 例如，如果用户是的成员**AuditUsers**分配给包的用户定义的角色，他们必须也是的成员`db_ssisadmin`， **db_ssisltduser**，或**db_ssisoperator**角色拥有对包的读取访问权限。  
  
 如果不为包分配用户定义角色，则对包的访问权限由固定数据库级角色确定。  
  
 如果你想要使用用户定义的角色，你必须将其添加到`msdb`数据库，然后才能将它们分配给包。 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中创建新的数据库角色。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据库级角色可授予 msdb 数据库中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 系统表的权限。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必须启动 （MSSQLSERVER 服务） 后，可以连接到数据库引擎以及访问`msdb`数据库。  
  
 为了向包分配角色，您需要完成以下任务。  
  
-   **打开对象资源管理器并连接到 Integration Services**  
  
     在使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]将角色分配给包之前，必须在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中打开对象资源管理器，并连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。  
  
     必须启动 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务才能连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。  
  
-   **将读取者角色和写入者角色分配给包**  
  
     可以将读取者角色和写入者角色分配给每个包。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [将读取者角色和写入者角色分配给包](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [创建用户定义的角色](../create-a-user-defined-role.md)  
  
-   [连接到 Integration Services](../connect-to-integration-services.md)  
  
  
