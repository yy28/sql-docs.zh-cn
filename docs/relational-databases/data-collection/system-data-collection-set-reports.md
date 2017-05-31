---
title: "系统数据收集组报表 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data collector [SQL Server], server activity
- server activity [SQL Server]
- reports [SQL Server], data collection
- reports [SQL Server], disk usage
- collection sets [SQL Server], reports
- data collector [SQL Server], reports
- reports [SQL Server], query statistics
- query statistics reports [SQL Server]
- disk usage reports [SQL Server]
ms.assetid: 0b126b8d-4fe7-443d-8a9a-c266350181e5
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 26ff209c4b0f52f3a25de54463a4fa4c2837d0a5
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="system-data-collection-set-reports"></a>系统数据收集组报表
  数据收集器提供了每个系统数据收集组的历史记录报表。 下面的每个报表都使用管理数据仓库中存储的数据：  
  
-   [磁盘使用情况摘要](#Disk)  
  
-   [查询统计信息历史记录](#Query)  
  
-   [服务器活动历史记录](#Server)  
  
 可以使用这些报表获取信息以监视系统功能和解决系统性能问题。  
  
##  <a name="Disk"></a> 磁盘使用情况摘要报表  
 磁盘使用情况摘要报表包含有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中所有数据库的磁盘空间使用情况的数据。 报表中提供的数据是使用磁盘使用情况收集组获取的，该收集组使用一般 T-SQL 查询收集器类型。  
  
 可以通过对象资源管理器访问磁盘使用情况摘要报表。 若要查看该报表，请展开“管理”文件夹，右键单击“数据收集”，依次指向“报表”和“管理数据仓库”，然后单击“磁盘使用情况摘要”。 有关详细信息，请参阅 [查看收集组报表 (SQL Server Management Studio)](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)实例中所有数据库的磁盘空间使用情况的数据。  
  
### <a name="disk-usage-collection-set-report"></a>磁盘使用情况收集组报表  
 磁盘使用情况收集组报表提供了用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中所有数据库的磁盘空间概览，并提供了其中每个数据库的数据文件和日志文件的增长趋势。  
  
-   摘要表显示了数据收集器所监视的服务器上安装的所有数据库的起始大小 (MB) 和当前大小。  
  
-   数据文件和日志文件的趋势和平均增长信息以图形和数值方式显示。  
  
#### <a name="disk-usage-collection-set---database-databasename-subreport"></a>磁盘使用情况收集组 - 数据库：<数据库名称> 子报表  
 当你在磁盘使用情况收集组报表的摘要表中单击特定数据库或日志文件的趋势线时，将显示磁盘使用情况收集组 - 数据库：*<database_name>* 子报表。 此报表提供了在一段时间内磁盘空间使用增长趋势的图形表示形式。 磁盘使用情况是按数据文件的已用空间、数据空间、未分配的空间和索引空间以及日志文件的已用空间和未使用空间组织和报告的。  
  
 图形下面的表列出了数据收集时间和相应的使用情况数据。  
  
#### <a name="disk-usage-for-database-databasename-subreport"></a>数据库的磁盘使用情况：<数据库名称> 子报表  
 在你单击磁盘使用情况收集组报表的摘要表中的数据库名称后，系统会显示“数据库 <database_name> 的磁盘使用情况”子报表。 此报表提供了数据库的数据文件和事务日志文件空间使用情况的数值和图形明细。 数据文件的空间使用情况是按分配给索引页、未分配的空间、数据页以及未使用空间的百分比进行分类的。 这些类别定义如下：  
  
|类别|定义|  
|--------------|----------------|  
|索引|用于保留索引页的磁盘空间量。|  
|未分配|可用于数据库的磁盘空间量，但尚未分配给任何对象。|  
|数据|由数据页使用的磁盘空间量。|  
|未使用|已分配给一个或多个对象的磁盘空间量，但尚未使用。|  
  
 事务日志文件的空间使用情况是按已用空间和未使用空间分类的。  
  
 如果自动增长和自动收缩事件已发生在数据库中，则将针对数据文件和日志文件报告这些事件。 报表将显示每个事件的开始时间和持续时间以及所产生的文件大小的更改。  
  
 将报告数据库中每个数据文件所使用的磁盘空间。 作为保留的空间报告的空间是已用空间量加上分配给文件但尚未使用的空间量。 按已用空间报告的空间是由排除分配的空间的文件当前使用的实际空间。  
  
##  <a name="Query"></a> 查询统计信息历史记录报表  
 查询统计信息历史记录报表包含查询执行统计信息。 此报表中使用的数据是通过查询统计信息收集组获取的，该收集组使用查询活动收集器类型。  
  
 可以通过对象资源管理器来访问查询统计信息历史记录报表。 若要查看报表，请展开“管理”文件夹，右键单击“数据收集”，依次指向“报表”和“管理数据仓库”，然后单击“查询统计信息历史记录”。 有关详细信息，请参阅 [查看收集组报表 (SQL Server Management Studio)](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)实例中所有数据库的磁盘空间使用情况的数据。  
  
### <a name="selecting-data-to-include-in-the-report"></a>选择要包含在报表中的数据  
 报表会包含整个数据收集期间内的查询执行统计信息。 可以使用两种方法浏览数据收集时间线以选择要查看的数据段。  
  
 **时间线控件和导航按钮**  
  
 使用时间线控件和导航按钮在时间线上移动或选择日期范围。 箭头按钮提供左右滚动功能，因此您可以在时间线上前后移动。 默认情况下，使用箭头在时间线上移动时，增量为 4 小时。 可以使用放大镜按钮将此时间增量扩大或缩小为以下值之一：15 分钟、1 小时、4 小时、12 小时或 24 小时。 当前选择的时间范围通过时间线的突出显示部分指示，并在时间线下方以文本形式显示。 每次单击时间线或使用导航按钮时，这些值以及报表中的数据都会相应更新。  
  
 **日历按钮**  
  
 使用日历按钮可指定要报告的数据的开始日期、开始时间和持续时间。  
  
#### <a name="query-statistics-history-report"></a>查询统计信息历史记录报表  
 “按总 CPU 时间排名靠前的查询”图形显示选定时间范围内的各个查询相对于总 CPU 使用率的开销。 若要显示不同的查询相对开销视图，请单击图形下面提供的以下超链接之一：“持续时间”、“I/O 总数”、“物理读取次数”或“逻辑写入次数”。  
  
 图形下方的表提供其他查询数据。 表中会列出图形中显示的每个查询的相应文本以及详细的统计信息。 请注意，各个图形条以及表中显示的每个查询都是活动链接。 单击某一活动链接可打开相应查询的查询详细信息子报表。  
  
#### <a name="query-details-subreport"></a>查询详细信息子报表  
 查询详细信息子报表提供完整的查询文本。 查询旁边有一个 **“编辑查询文本”** 超链接。 可以单击此链接在查询编辑器中打开该查询。 查询下面的表中提供了查询执行统计信息，例如，每次查询执行的平均持续时间。  
  
 将显示查询计划和每次执行的平均持续时间图形。 若要显示不同的查询计划相对开销视图，请单击图形下面显示的任一超链接： **“持续时间”**、 **“物理读取次数”**或 **“逻辑写入次数”**。 图形线将处于活动状态，您可以单击任意点打开查询计划详细信息子报表。  
  
 图形下面的表根据每次执行时使用的 CPU 时间显示前 10 个查询计划。 “计划编号”列中的每个数字都是一个活动链接，可以单击这样的链接以打开查询计划详细信息子报表。  
  
#### <a name="query-plan-details-subreport"></a>查询计划详细信息子报表  
 此报表显示查询计划的相关信息。 除了可用于编辑查询和查看执行统计信息外，此报表还提供有关查询计划的详细信息。 **“查看图形查询执行计划”** 超链接可打开当前查询的执行计划的图形表示形式。  
  
## <a name="server-activity-history-report"></a>服务器活动历史记录报表  
 服务器活动历史记录报表包含有关服务器和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的资源消耗情况和服务器活动的数据。 此报表中提供的数据是由服务器活动收集组收集的，该收集组使用一般 T-SQL 查询收集器类型和性能计数器收集器类型。  
  
 可以通过对象资源管理器来访问服务器活动历史记录报表。 若要查看此报表，请展开“管理”文件夹，右键单击“数据收集”，依次指向“报表”和“管理数据仓库”，然后单击“服务器活动历史记录”。 有关详细信息，请参阅 [查看收集组报表 (SQL Server Management Studio)](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)实例中所有数据库的磁盘空间使用情况的数据。  
  
### <a name="selecting-data-to-include-in-the-report"></a>选择要包含在报表中的数据  
 报表会将整个数据收集期间内发生的服务器活动纳入其中。 可以使用两种方法浏览数据收集时间线以选择要查看的数据段。  
  
 **时间线控件和导航按钮**  
  
 使用时间线控件和导航按钮在时间线上移动或选择日期范围。 箭头按钮提供左右滚动功能，因此您可以在时间线上前后移动。 默认情况下，使用箭头在时间线上移动时，增量为 4 小时。 可以使用放大镜按钮将此时间增量扩大或缩小为以下值之一：15 分钟、1 小时、4 小时、12 小时或 24 小时。 当前选择的时间范围通过时间线的突出显示部分指示，并在时间线下方以文本形式显示。 每次单击时间线或使用导航按钮时，这些值以及报表中的数据都会相应更新。  
  
 **日历按钮**  
  
 使用日历按钮可指定要报告的数据的开始日期、开始时间和持续时间。  
  
###  <a name="Server"></a> 服务器活动历史记录报表  
 服务器活动历史记录报表显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例和主机操作系统的服务器活动的初始视图。  
  
 下表介绍了报表中显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和系统活动相关信息的图形以及可以通过这些图形访问的详细子报表。  
  
|图形|报表说明|  
|-----------|------------------------|  
|%CPU|通过单击 %CPU 图形中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或系统图形线上的任意点可访问以下子报表。<br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** ：查询统计信息历史记录报表提供了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中费用最高昂的查询的图。 图形下方的表将列出这些查询，并包含其中每一查询的统计数据。 可以单击某一查询获取其他详细信息。<br /><br /> **系统**：系统 CPU 使用率报表提供了每个处理器的 %CPU 时间的图，并以表格格式显示了每个进程的统计数据。|  
|内存使用量|通过单击内存使用量图形中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或系统图形线上的任意点可访问以下子报表。<br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** ： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存使用量报表按类型提供了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程内存使用量、内存计数器以及内部内存占用情况的图，并在表中按组件类型显示了平均内存使用量数据。<br /><br /> **系统**：系统内存使用量报表提供了内存使用量以及缓存和页面命中率的图，并在表中显示了每个进程的工作集和专用字节的相关信息。|  
|磁盘 I/O 使用情况|通过单击磁盘 I/O 使用情况图形中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或系统图形线上的任意点可访问以下子报表。<br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** ： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁盘 I/O 使用情况报表提供了磁盘响应时间和磁盘传输速度的图。 其他表格提供按照磁盘、数据库和文件排列的虚拟文件统计信息。<br /><br /> **系统**：系统磁盘使用情况报表提供了磁盘响应时间、平均磁盘队列长度以及磁盘传输速度的图，并在表中显示了每个进程的 I/O 写入和读取操作的相关信息。|  
|网络使用情况|没有提供额外的报表。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 等待|“ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 等待”图形显示按照等待类别排列的所执行线程遇到的等待。 单击该图形中的任意段可访问详细报表。 除了提供时间范围较窄的图形 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 等待统计信息外，此报表还以表格形式提供等待类别的相关信息。 对于每个类别（如 CPU 及其子类别），该表格显示等待数、等待时间以及占总等待时间的百分比。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 活动|可通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 活动图形访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 活动的不同方面。 通过单击 SQL 编译数/秒图形线上的点获取的报表如下所示：<br /><br /> <br /><br /> 连接和会话<br /><br /> 请求<br /><br /> 计划缓存命中率<br /><br /> tempdb 特征|  
  
## <a name="see-also"></a>另请参阅  
 [数据收集](../../relational-databases/data-collection/data-collection.md)   
 [查看收集组报表 (SQL Server Management Studio)](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
  
