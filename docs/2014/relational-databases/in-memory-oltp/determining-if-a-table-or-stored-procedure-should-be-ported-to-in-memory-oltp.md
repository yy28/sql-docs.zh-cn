---
title: 确定表或存储过程是否应移植到内存中 OLTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- Analyze, Migrate, Report
- AMR
ms.assetid: c1ef96f1-290d-4952-8369-2f49f27afee2
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e517cff394bc0c813e34763469f75147a0a16c5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050235"
---
# <a name="determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp"></a>确定表或存储过程是否应移植到内存中 OLTP
  中的事务性能收集器 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 可帮助您评估内存中 OLTP 是否将改进数据库应用程序的性能。 事务性能分析报告还指示在应用程序中启用内存中 OLTP 所必须完成的工作量。 在你标识了要移植到内存中 OLTP 的基于磁盘的表之后，可以使用 [内存优化顾问](memory-optimization-advisor.md)帮助你迁移表。 同样， [Native Compilation Advisor](native-compilation-advisor.md) 帮助您将存储过程移植到本机编译的存储过程。  
  
 本主题讨论如何：  
  
-   配置管理数据仓库。  
  
-   配置数据收集。  
  
-   生成事务性能分析报告以便标识性能至关重要的表和存储过程。  
  
 有关迁移方法的信息，请参阅 [内存中 OLTP - 常见的工作负荷模式和迁移注意事项](https://msdn.microsoft.com/library/dn673538.aspx)。  
  
 事务性能收集器和事务性能分析报告可帮助您完成下列任务：  
  
-   分析工作负荷以确定内存中 OLTP 能否提升性能。 事务性能收集器收集并评估工作负荷的性能特征。 . 之后，事务性能分析报告会建议可从转换到内存中 OLTP 获益最多的表和存储过程。  
  
-   帮助您规划和执行到内存中 OLTP 的迁移。 从基于磁盘的表到内存优化表的迁移路径可能比较费时。 内存优化顾问可帮助您找到表中的不兼容之处（必须在将表迁移到内存中 OLTP 之前予以解决）。 此外，内存优化顾问还可帮助您了解将表迁移到内存优化表会对应用程序产生何种影响。  
  
     在规划到内存中 OLTP 的迁移时，或每当您需要将某些表或存储过程迁移到内存中 OLTP 时，都可了解应用程序是否可从内存中 OLTP 获益。  
  
    > [!IMPORTANT]  
    >  数据库的性能取决于多种因素，不是所有这些因素都能被事务性能收集器发现和度量。 因此，事务性能分析报告不保证实际性能收益会符合其预测（如果作出任何预测）。  
  
 当你在安装时选择 "**管理工具-基本**" 或 "**管理工具-高级**" 时，会安装事务性能收集器和生成事务性能分析报告的功能 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 。  
  
## <a name="best-practices"></a>最佳实践  
 下面的流程图给出了建议的工作流程。 黄色节点表示可选过程：  
  
 ![AMR 工作流](../../database-engine/media/amr-1.gif "AMR 工作流")  
  
 可使用任意方法设立性能基准，包括但不限于使用性能计数器日志或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 活动监视器。 可在性能基准和比较中使用的信息包括：  
  
-    的 CPU 占用率。  
  
-    的内存占用率。  
  
-    的 I/O 活动。  
  
-   处理事务时，实例的事务吞吐量。  
  
 事务性能收集器每 15 分钟捕获数据。 若要获得稳定的结果，运行事务性能收集器至少 1 小时。 若要获得最佳结果，请根据需要运行尽可能长时间的事务性能收集器，以便捕获针对您的主要情形的数据。 只有在完成数据收集后，才生成事务性能分析报告。  
  
 将事务性能收集器配置为在生产中在您的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上运行，并且在您的开发（测试）环境中收集 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上的数据以便确保最小的系统开销。 有关如何在远程实例上的管理数据仓库数据库中保存数据的信息 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，请参阅[在远程 SQL Server 实例上配置数据收集](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md#xxx)。  
  
## <a name="performance-impacts"></a>性能影响  
 事务性能收集器由两个数据收集组构成：  
  
-   表使用情况分析  
  
-   存储过程分析  
  
 事务性能收集器的收集组每 15 分钟从三个动态管理视图 (DMV) 设置收集数据，并且将数据上载到配置为充当管理数据仓库的数据库。 上载收集的数据会产生最小的性能影响。  
  
## <a name="use-the-transaction-performance-collector"></a>使用事务性能收集器  
 以下步骤需要 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]（包含在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中）。  
  
> [!IMPORTANT]  
>  不要在探查期间更改架构（例如，添加或删除数据库或创建或删除表）。 如果您在收集数据时更改数据库的架构，则报告中可能不会准确地包含该数据库。  
  
### <a name="configure-management-data-warehouse"></a>配置管理数据仓库  
 必须配置管理数据仓库以便使用事务性能收集器。  
  
 将对其收集数据的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例（探查对象）的版本应与配置管理数据仓库的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本相同，或低于后者。  
  
1.  在对象资源管理器中，展开 **“管理”**。  
  
2.  右键单击 "**数据收集**" 并选择 "**任务**"，然后**配置 "管理数据仓库**"。 "**配置管理数据仓库向导**" 随即开始。  
  
3.  单击 "**下一步**" 以选择将充当管理数据仓库的数据库。  
  
4.  单击 "**新建**" 以创建一个新数据库来保存配置文件数据。 数据库创建完成后，在向导中单击 "**下一步**"。  
  
5.  在向导中的下一步，可以添加用户并登录。 可以将登录映射到 MDW 实例的角色成员身份。 从本地实例收集数据时无需执行该操作。 如果不是从本地实例收集数据，则可将数据库角色成员身份 `mdw_admin` 授予将运行待探查事务的帐户。 完成后单击“下一步”。  
  
6.  请确保 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理正在运行。  
  
7.  在下一个屏幕上，单击 "**完成**" 退出向导。  
  
### <a name="configure-data-collection-on-a-local-ssnoversion-instance"></a>在本地 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上配置数据收集  
 数据收集需要启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理。 在一个服务器上，您仅需配置一个数据收集器。  
  
 可以在 SQL Server 2012 或更高版本的上配置数据收集器 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 若要配置数据收集以便上载到同一实例上的管理数据仓库数据库，请执行以下步骤：  
  
1.  在**对象资源管理器**中，展开 "**管理**"。  
  
2.  右键单击 "**数据收集**"，选择 "**任务**"，然后**配置 "数据收集**"。 "**配置数据收集向导**" 随即开始。  
  
3.  单击 "**下一步**" 以选择将收集配置文件数据的数据库。  
  
4.  选择当前 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例，然后在该实例上选择管理数据仓库数据库。  
  
5.  在标记为 "**选择要启用的数据收集器集**" 的框中，选择 "**事务性能收集组**"。 操作完成后，单击“下一步”。  
  
6.  验证所做的选择。 单击 "**上一步**" 以修改设置。 完成操作后，请单击 **“完成”** 。  
  
###  <a name="configure-data-collection-on-a-remote-ssnoversion-instance"></a><a name="xxx"></a>在远程实例上配置数据收集 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 数据收集要求在收集该数据的实例上启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理。  
  
 可以在 SQL Server 2012 或更高版本的上配置数据收集器 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 需要使用用于数据收集器的正确凭据建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理，以便将数据上载到其他实例（非待探查事务所在实例）上的管理数据仓库数据库。 若要启用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理，必须首先使用启用域的登录建立凭据。 该启用域的登录必须是管理数据仓库数据库的 `mdw_admin` 组的成员。 有关如何创建凭据的信息，请参阅[如何：创建凭据（SQL Server Management Studio）](../security/authentication-access/create-a-credential.md) 。  
  
 若要配置数据收集以便上载到不同实例上的管理数据仓库数据库，请执行以下步骤：  
  
1.  在包含要迁移到内存中 OLTP 的基于磁盘的对象的实例上，展开对象资源管理器中的 "**管理**" 节点。  
  
2.  右键单击 "**数据收集**"，然后选择 "**任务**"，然后**配置 "数据收集**"。 "**配置数据收集向导**" 随即开始。  
  
3.  单击 "**下一步**" 以选择将收集配置文件数据的数据库。  
  
4.  确保管理数据仓库数据库在其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上存在。  
  
5.  选择另一 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例，然后在该实例上选择管理数据仓库数据库。  
  
     将对其收集数据的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例（探查对象）的版本应与配置管理数据仓库的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本相同，或低于后者。  
  
6.  在标记为 "**选择要启用的数据收集器集**" 的框中，选择 "**事务性能收集组**"。  
  
7.  选择 "**使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理程序代理进行远程上载**"。  
  
8.  操作完成后，单击“下一步”。  
  
9. 选择代理。  
  
     如果要创建新的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理的代理帐户，请执行以下步骤：  
  
    1.  单击 "**新建**" 以显示 "**新建代理帐户**" 对话框。  
  
    2.  在 "**新建代理帐户**" 对话框中，输入代理名称，选择凭据，并选择性地输入说明。 然后单击 "**主体**"。  
  
    3.  单击 "**添加**"，然后选择 " **Msdb**角色"。  
  
    4.  选择 `dc_proxy` 并单击 **"确定"**。 然后再次单击“确定”****。  
  
     选择正确的代理后，单击 "**下一步**"。  
  
10. 若要配置系统收集组，请检查**系统收集组**，然后单击 "**下一步**"。  
  
11. 验证所做的选择。 单击 "**上一步**" 以修改设置。 完成后，完成**完成**。  
  
 数据收集组现已配置完成并运行在实例上。  
  
### <a name="generate-reports"></a>生成报告  
 您可以通过右键单击管理数据仓库的数据库，然后依次选择 "**报表**"、"**管理数据仓库**"、"**事务性能分析概述**" 来生成事务性能分析报告。  
  
 该报告收集有关工作负荷服务器上的所有用户数据库的信息。 如果您的管理数据仓库 (MDW) 数据库在本地计算机上，会在报告中看到 MDW 数据库。  
  
 CPU 时间与占用时间的比值较高的存储过程适合迁移。 该报告显示所有表引用，因为本机编译的存储过程只能引用内存优化的表，这可能加大迁移成本。  
  
 表的详细报告包含三个部分：  
  
-   扫描统计信息部分  
  
     本部分包含一个表，其中显示已收集的有关数据库表扫描的统计信息。 列包括：  
  
    -   总访问次数百分比。 对此表的扫描和查询次数相对于整个数据库的活动的百分比。 这个比例越高，使用此表的频率相对于数据库中的其他表就越大。  
  
    -   查找统计数据/范围扫描统计数据。 此列记录在探查期间对表执行的点查询和范围扫描（索引扫描和表扫描）次数。 每事务的平均值为估计值。  
  
    -   互操作提升和本机提升。 这些列估计在将表转换为内存优化表时，点查询或范围扫描将会获得的性能优势量。  
  
-   争用统计数据部分  
  
     本部分包含一个表，其中显示数据库表的争用。 有关数据库闩锁和锁的详细信息，请参阅[锁定体系结构](https://msdn.microsoft.com/library/aa224738\(v=sql.80\).aspx)。 这些列如下所示：  
  
    -   总等待百分比。 此数据库表上闩锁和锁等待数占数据库活动的百分比。 这个比例越高，使用此表的频率相对于数据库中的其他表就越大。  
  
    -   闩锁统计信息。 这些列记录涉及此表的查询的闩锁等待数。 有关闩锁的信息，[请参阅闩锁。](https://msdn.microsoft.com/library/aa224727\(v=SQL.80\).aspx) 此数值越高，表的闩锁争用就越多。  
  
    -   锁定统计信息。 这组列记录对此表的查询的页锁定获取和等待次数。 有关锁的详细信息，请参阅[了解 SQL Server 中的锁定](https://msdn.microsoft.com/library/aa213039\(v=SQL.80\).aspx)。 等待越多，对表的锁定争用就越多。  
  
-   迁移难度部分  
  
     本部分包含一个表，其中显示将此数据库表转换为内存优化表的困难程度。 难度等级越高，转换表的难度就越大。 若要查看转换此数据库表的详细信息，请使用[内存优化顾问](memory-optimization-advisor.md)。  
  
 "表详细信息" 报告中的扫描和争用统计信息将从[sys. dm_db_index_operational_stats &#40;transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql)进行收集和聚合。  
  
 存储过程的详细报告包含两个部分：  
  
-   执行统计信息部分  
  
     本部分包含一个表，其中显示与已收集的存储过程执行相关的统计信息。 这些列如下所示：  
  
    -   缓存的时间。 高速缓存此执行计划的时间。 如果存储过程删除计划高速缓存并重新输入，这里将有每个缓存的时间。  
  
    -   总 CPU 时间。 存储过程在探查期间使用的总 CPU 时间。 此数值越高，存储过程使用的 CPU 就越多。  
  
    -   总执行时间。 存储过程在探查期间使用的执行时间总量。 此数值与 CPU 时间之间的差值越高，存储过程使用 CPU 的效率就越低。  
  
    -   总高速缓存失误数。 探查期间由存储过程执行引起的高速缓存失误数（从物理存储读取）。  
  
    -   执行计数。 在探查期间，此存储过程执行的次数。  
  
-   表引用部分  
  
     本部分包含一个表，其中显示此存储过程引用的那些表。 在将存储过程转换为本机编译的存储过程前，所有这些表必须转换为内存优化表，且它们必须位于同一服务器和数据库上。  
  
 有关存储过程详细信息的执行统计信息，请从[sys.databases&#41;dm_exec_procedure_stats &#40;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql)收集和聚合。 这些引用是从[sql_expression_dependencies &#40;transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)获取的。  
  
 若要查看有关如何将存储过程转换为本机编译的存储过程的详细信息，请使用[本机编译顾问](native-compilation-advisor.md)。  
  
## <a name="see-also"></a>另请参阅  
 [迁移到内存中 OLTP](migrating-to-in-memory-oltp.md)  
  
  
