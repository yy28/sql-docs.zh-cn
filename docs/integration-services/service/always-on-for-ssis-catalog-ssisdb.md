---
title: "Always On for SSIS Catalog (SSISDB) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.alwayson.f1"
ms.assetid: 7f089455-35ee-4c13-884e-9254b685d07d
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# Always On for SSIS Catalog (SSISDB)
  AlwaysOn 可用性组功能是一个高可用性和灾难恢复解决方案，可以提供替代数据库镜像的企业级方案。 可用性组针对一组离散的用户数据库（称为可用性数据库，它们共同实现故障转移）支持故障转移环境。 有关详细信息，请参阅 [AlwaysOn 可用性组](https://msdn.microsoft.com/library/hh510230.aspx)。  
  
 为了对 SSIS 目录 (SSISDB) 及其内容（项目、包、执行日志等）提供高可用性，可以将 SSISDB 数据库（与其他任何用户数据库相同）添加到 AlwaysOn 可用性组。 当发生故障转移时，其中一个辅助节点将自动成为新的主节点。  
 
 > [!IMPORTANT]  发生故障转移时，正在运行的包不会重启或恢复。 
 
 **本主题内容：**  
  
1.  [先决条件](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#prereq)  
  
2.  [为 AlwaysOn 配置 SSIS 支持](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Firsttime)  
  
3.  [在可用性组中升级 SSISDB](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Upgrade)  
  
##  <a name="a-nameprereqa-prerequisites"></a><a name="prereq"></a>先决条件  
 在为 SSISDB 数据库启用 AlwaysOn 支持之前，必须执行以下先决条件步骤。  
  
1.  设置 Windows 故障转移群集。 请参阅 [安装适用于 Windows Server 2012 的故障转移群集功能和工具](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 的博客文章以获取相关说明。 应在所有群集节点上安装功能和工具。  
  
2.  在群集的每个节点上安装具有 Integration Services (SSIS) 功能的 SQL Server 2016。  
  
3.  为每个 SQL Server 实例启用 AlwaysOn 功能。 有关详细信息，请参阅 [启用 AlwaysOn 可用性组](https://msdn.microsoft.com/library/ff878259.aspx) 。  
  
##  <a name="a-namefirsttimea-configure-ssis-support-for-always-on"></a><a name="Firsttime"></a>为 AlwaysOn 配置 SSIS 支持  
  
-   [步骤 1：创建 Integration Services 目录](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step1)  
  
-   [步骤 2：将 SSISDB 添加到 AlwaysOn 可用性组](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step2)  
  
-   [步骤 3：为 AlwaysOn 启用 SSIS 支持](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step3)  
  
> [!IMPORTANT]  
>  -   必须在可用性组的 **主节点** 上执行这些步骤。  
> -   在将 SSISDB 添加到 AlwaysOn 组后，必须启用 **AlwaysOn 的 SSIS 支持** 。  
  
###  <a name="a-namestep1a-step-1-create-integration-services-catalog"></a><a name="Step1"></a>步骤 1：创建 Integration Services 目录  
  
1.  启动 **SQL Server Management Studio** 并连接到你想要设置为适用于 SSISDB 的 AlwaysOn 高可用性组的 **主节点** 的群集中的 SQL Server 实例。  
  
2.  在“对象资源管理器”中，展开服务器节点，右键单击“Integration Services 目录”节点，然后单击“创建目录”。  
  
3.  单击 **“启用 CLR 集成”**。 该目录使用 CLR 存储过程。  
  
4.  单击“在 SQL Server 启动时启用自动执行 Integration Services 存储过程”  ，使 [catalog.startup](https://msdn.microsoft.com/library/hh230984.aspx) 存储过程在每次重启 SSIS 服务器后运行。 该存储过程对 SSISDB 目录的操作状态进行维护。 它可以修复当 SSIS 服务器实例出现故障时正在运行的任何包的状态。  
  
5.  输入 **密码**，然后单击“确定” 。 该密码保护用于对目录数据进行加密的数据库主密钥。 将该密码保存在安全的位置。 同时建议您也备份数据库主密钥。 有关详细信息，请参阅 [备份数据库主密钥](https://msdn.microsoft.com/library/aa337546.aspx)。  
  
###  <a name="a-namestep2a-step-2-add-ssisdb-to-an-always-on-availability-group"></a><a name="Step2"></a>步骤 2：将 SSISDB 添加到 AlwaysOn 可用性组  
 将 SSISDB 数据库添加到 AlwaysOn 可用性组的方法与将任何其他用户数据库添加到可用性组的方法几乎相同。 请参阅 [使用可用性组向导](https://msdn.microsoft.com/library/hh403415.aspx)。  
  
 你需要提供在“新建可用性组”  向导的“选择数据库”  页面中创建 SSIS 目录时指定的密码。  
  
 ![New Availability Group](../../integration-services/service/media/ssis-newavailabilitygroup.png "New Availability Group")  
  
###  <a name="a-namestep3a-step-3-enable-ssis-support-for-always-on"></a><a name="Step3"></a>步骤 3：为 AlwaysOn 启用 SSIS 支持  
 创建 Integration Service 目录后，右键单击“Integration Service 目录”节点，然后单击“启用 AlwaysOn 支持…”。 应该能看到以下“为 AlwaysOn 启用支持”的对话框。 如果此菜单被禁用，请确认已安装所有必备组件，然后单击“刷新” 。  
  
 ![Enable Support for AlwaysOn](../../integration-services/service/media/ssis-enablesupportforalwayson.png "Enable Support for AlwaysOn")  
  
> [!WARNING]  
>  为 AlwaysOn 启用 SSIS 支持之前，不支持 SSISDB 数据库的自动故障转移。  
  
 从 AlwayOn 可用性组新添加的次要副本将在表中显示。 单击 **“连接…”** 按钮，然后输入身份验证凭据以连接到副本。 用户帐户必须是每个副本上 sysadmin 组的成员才可启用 SSIS AlwaysOn 支持。 成功连接到每个副本后，单击“确定”按钮以启用对 AlwaysOn 的 SSIS 支持。  
  
##  <a name="a-nameupgradea-upgrading-ssisdb-in-an-availability-group"></a><a name="Upgrade"></a>在可用性组中升级 SSISDB  
 如果正在从以前的版本升级 SQL Server，并且 SSISDB 位于 AlwaysOn 可用性组中，则“AlwaysOn 可用性组中的 SSISDB 检查”规则可能会阻止你的升级。 出现这种阻止是因为升级是以单用户模式运行的，而可用性数据库必须是多用户数据库。 因此，在升级或修补过程中，所有可用性数据库（包括 SSISDB）均将处于脱机状态，不会进行升级或修补。 若要使升级继续，必须先从可用性组中删除 SSISDB，然后升级或修补每一个节点，再将 SSISDB 添加回可用性组中。  
  
 如果被“AlwaysOn 可用性组中的 SSISDB 检查”规则阻止，则必须按照这些步骤来升级 SQL Server。  
  
1.  从可用性组中删除 SSISDB 数据库。 有关详细信息，请参阅[将辅助数据库从可用性组删除 (SQL Server)](../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md) 和[将主数据库从可用性组删除 (SQL Server)](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)。  
  
2.  在升级向导中单击“重新运行”。 “AlwaysOn 可用性组中的 SSISDB 检查”规则将会通过。  
  
3.  单击“下一步”  以继续升级。  
  
4.  升级所有节点后，将 SSISDB 数据库添加回 AlwaysOn 可用性组中。 有关详细信息，请参阅[将数据库添加到可用性组 (SQL Server)](../../database-engine/availability-groups/windows/add-a-database-to-an-availability-group-sql-server.md)。  
  
 如果升级 SQL Server 时没有受到阻止，并且 SSISDB 位于 AlwaysOn 可用性组中，则在升级 SQL Server 数据库引擎之后必须单独升级 SSISDB。 按照以下过程中所述，使用 SSIS 升级向导升级 SSISDB。  
  
1.  将 SSISDB 数据库移出可用性组，或者如果 SSISDB 是可用性组中唯一的数据库，则删除可用性组。 必须启动可用性组的 **主节点** 上的“SQL Server Management Studio”  来执行此任务。  
  
2.  从所有 **副本节点**删除 SSISDB 数据库。  
  
3.  在 **主节点**上升级 SSISDB 数据库。 在 SQL Server Management Studio 内的“对象资源管理器”中，展开“Integration Services 目录”，右键单击“SSISDB”，然后选择“数据库升级”。 按照“SSISDB 升级向导”  中的说明来升级数据库。 必须在 **主节点** 上本地启动 **SSIDB 升级向导**。  
  
4.  按照 [步骤 2：将 SSISDB 添加到 AlwaysOn 可用性组](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step2) 中的说明将 SSISDB 添加回可用性组。  
  
5.  按照 [步骤 3：为 AlwaysOn 启用 SSIS 支持](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step3)中的说明执行。  
  
  