---
title: 配置管理数据仓库 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.datacollection.wizard_completecfg.f1
- sql13.swb.dc.datacollection.wizard_config.f1
- sql13.swb.dc.datacollection.wizard_finish.f1
- sql13.swb.dc.datacollection.wizard_maploginuser.f1
- sql13.swb.dc.datacollection.wizard_choosemdw.f1
- sql13.swb.dc.datacollection.wizard_welcome.f1
- sql13.swb.dc.datacollection.wizard_createmdw.f1
helpviewer_keywords:
- data warehouse [SQL Server], multiple instances
- data warehouse [SQL Server], configuring
- Configure Management Data Warehouse Wizard
- management data warehouse, configuring
ms.assetid: 23a584f3-c5e1-414c-9afe-73cd7efbda4b
caps.latest.revision: 28
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48225263d322b901baa87084b47bedaf36fcc601
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33145198"
---
# <a name="configure-the-management-data-warehouse-sql-server-management-studio"></a>配置管理数据仓库 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题介绍如何配置管理数据仓库以支持使用数据收集器的单个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的数据存储。 这些实例可能位于相同或不同的服务器上。 本主题还提供针对 [配置管理数据仓库向导](#Wizard) 对话框的用户界面的说明。 有关配置数据收集器的信息，请参阅 [Configure Properties of a Data Collector](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md)。  
  
> [!NOTE]  
>  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理配置为使用其中一个系统服务帐户（Local System、Network Service 或 Local Service）运行，且创建管理数据仓库的实例与数据收集器的实例不同，则必须将收集组配置为使用代理将数据上载到管理数据仓库。  
  
### <a name="configure-the-management-data-warehouse-on-a-single-instance-or-multiple-instances-of-includessnoversionincludesssnoversion-mdmd"></a>配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  请确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理正在运行。  
  
2.  在对象资源管理器中，展开 **“管理”** 节点。  
  
3.  右键单击“数据收集”，展开“任务”，然后单击“配置管理数据仓库”。  
  
4.  使用 [配置管理数据仓库向导](#Wizard) 创建一个管理数据仓库，配置登录名，启用数据收集，然后启动 **“系统数据收集组”**。  
  
     若要配置多个实例，请继续执行步骤 5。  
  
    > [!NOTE]  
    >  在数据收集器安装在使用同一管理数据仓库的多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的部署中，使用代理是最佳做法。  
  
5.  在另一个实例上打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，然后执行以下任意一项操作：  
  
    -   使用配置管理数据仓库向导为现有的管理数据仓库配置数据收集。  
  
    -   右键单击“数据收集”，然后单击“属性”。 在 **“常规”** 选项卡上，指定现有的管理数据仓库以及安装该管理数据仓库的服务器。  
  
6.  重复步骤 5 直至将使用该数据收集的所有数据库实例均配置为将数据上载到共享的管理数据仓库。  
  
####  <a name="Wizard"></a> 配置管理数据仓库向导  
 **“欢迎”页**  
  
 欢迎页是配置数据收集向导的起始页。 是否显示此页是可选的。  
  
 **不再显示此起始页。**  
 选择此选项可在下一次启动配置数据收集向导时不显示该页。  
  
 **“配置管理数据仓库存储”页**  
  
 使用此页可选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库服务器和管理数据仓库。 管理数据仓库是将存储收集的数据的关系数据库。  
  
> [!NOTE]  
>  您必须拥有相应级别的权限才能在服务器上创建管理数据仓库。 有关详细信息，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)。 您还必须拥有为管理数据仓库角色创建登录名的相应级别权限。  
  
 **服务器名称**  
 指定将承载管理数据仓库的服务器的名称。  
  
 配置管理数据仓库时， **“服务器名称”** 始终为本地服务器的名称且不能修改。  
  
 **数据库名称**  
 指定将存储收集的数据的关系数据库。 从列表中选择现有数据库，或单击 **“新建”** 通过 **“新建数据库”** 对话框创建新的数据库。  
  
 只有在配置数据收集组时， **“新建”** 选项才可用。  
  
 **“映射登录名和用户”页**  
  
 使用此页可以将登录名映射到管理数据仓库的数据库用户角色。  
  
 **映射到此登录名的用户**  
 显示将承载管理数据仓库的服务器中的现有登录名。 每一行包含一个可编辑的 **“映射”** 复选框、一个 **“登录”** 名和一个登录名的 **“类型”** 。  
  
 可通过为某个登录名选中 **“映射”** 复选框来指定该登录名。  
  
 **以下项的数据库角色成员身份：***\<数据仓库名称>*  
 通过单击以下一个或多个选项旁边的复选框，选择登录名映射到的管理数据仓库角色：  
  
-   **mdw_admin**  
  
-   **mdw_reader**  
  
-   **mdw_writer**  
  
 **新建登录名**  
 打开“登录名 - 新建”对话框并为管理数据仓库创建新的登录名。  
  
 **“完成向导”页**  
  
 使用此页可验证和完成数据收集配置。 显示在查看窗口中的树用于说明将应用的配置以及单击 **“完成”** 时将执行的操作。  
  
 **“配置数据收集向导进度”页**  
  
 使用此页可查看每个配置步骤的结果。  
  
 **详细信息**  
 每个配置步骤在“详细信息”网格中显示为一行。 每一行均包含描述相应步骤的 **“操作”** 列和指示该步骤成功或失败的 **“状态”** 列。 如果有错误，则在 **“消息”** 列中会显示消息。  
  
 **停止**  
 停止向导的处理。  
  
 **报告**  
 查看数据收集配置的报告。 提供了以下报告选项：  
  
-   查看报告  
  
-   将报告保存到文件  
  
-   将报告复制到剪贴板  
  
-   将报告作为电子邮件发送  
  
 **关闭**  
 关闭向导。  
  
## <a name="see-also"></a>另请参阅  
 [sp_syscollector_enable_collector (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [数据收集](../../relational-databases/data-collection/data-collection.md)   
 [管理数据收集](../../relational-databases/data-collection/manage-data-collection.md)  
  
  
