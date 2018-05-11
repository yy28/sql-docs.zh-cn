---
title: AMO 其他类和方法 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6af27bdf70978e0a29c39a3af2d421dca2437cfe
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="amo-other-classes-and-methods"></a>AMO 其他类和方法
  本部分包含公共类，并不特定于 olap 数据或数据挖掘，并且在管理或管理中的对象时，很有帮助[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 它们包括诸如存储过程、跟踪、异常、备份和还原等功能。  
  
 本主题包含以下各节：  
  
-   [程序集对象](#Assembly)  
  
-   [备份和还原方法](#Backup)  
  
-   [跟踪对象](#Traces)  
  
-   [CaptureLog 类和 CaptureXML 属性](#CaptureLog)  
  
-   [AMOException 异常类](#AMO)  
  
 下图显示了本主题中介绍的类之间的关系。  
  
 ![AMO 其他类](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-otherclasses.gif "AMO 其他类")  
  
##  <a name="Assembly"></a> 程序集对象  
 <xref:Microsoft.AnalysisServices.Assembly> 对象的创建方法是：将其添加到服务器的程序集集合中，然后使用 Update 方法将 <xref:Microsoft.AnalysisServices.Assembly> 对象更新到服务器中。  
  
 若要删除<xref:Microsoft.AnalysisServices.Assembly>对象时，它具有要使用的 Drop 方法删除<xref:Microsoft.AnalysisServices.Assembly>对象。 从数据库的程序集集合中删除 <xref:Microsoft.AnalysisServices.Assembly> 对象不会删除程序集，只会使您在下次运行应用程序之前在应用程序中看不到它。  
  
 有关可用方法和属性的详细信息，请参阅<xref:Microsoft.AnalysisServices.Assembly>中<xref:Microsoft.AnalysisServices>。  
  
> [!IMPORTANT]  
>  COM 程序集可能会造成安全风险。 由于此风险和其他注意事项， [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]中不推荐使用 COM 程序集。 未来版本可能不支持 COM 程序集。  
  
##  <a name="Backup"></a> 备份和还原方法  
 Backup 和 Restore 方法分别用于创建 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库的副本及使用副本恢复数据库。 Backup 方法属于 <xref:Microsoft.AnalysisServices.Database> 对象，Restore 方法属于 <xref:Microsoft.AnalysisServices.Server> 对象。  
  
 只有服务器管理员和数据库管理员可以执行数据库的备份。 只有服务器管理员可以将数据库还原到与其备份之前所在服务器不同的服务器中。 数据库管理员只有在拥有某个现有数据库时，才可以通过覆盖该数据库来还原数据库。 如果数据库还原时带有其原始安全定义，则还原之后，数据库管理员可能会失去对还原后的数据库的访问权限。  
  
 数据库备份文件必须有 .abf 扩展名。  
  
### <a name="backup-method"></a>Backup 方法  
 若要备份数据库，请使用数据库对象的 Backup 方法，并以备份文件的名称作为参数。  
  
##### <a name="default-values"></a>默认值：  
 AllowOverwrite=**false**  
  
 BackupRemotePartitions=**false**  
  
 Security=**CopyAll**  
  
 ApplyCompression=**true**  
  
### <a name="restore-method"></a>Restore 方法  
 若要将数据库还原到服务器，请使用服务器的 Restore 方法，并以备份文件作为参数。  
  
##### <a name="default-values"></a>默认值：  
 AllowOverwrite=**false**  
  
 DataSourceType=**Remote**  
  
 Security=**CopyAll**  
  
##### <a name="restrictions"></a>限制  
  
1.  本地分区不能还原为远程分区。  
  
2.  远程分区不能还原为本地分区，但是可以还原到与其备份之前所在服务器不同的服务器中。  
  
### <a name="common-parameters-and-properties-for-backup-and-restore-methods"></a>Backup 和 Restore 方法的常用参数和属性  
  
-   **文件**到/从是备份 （UNC 名称） 的文件的名称。  
  
-   **位置**指定特定于服务器备份的信息，例如**BackupFile**。这可以用来指定远程数据库的单独备份文件。  
  
-   **DatasourceID**指定远程服务器中的从属的数据库 ID。  
  
-   **ConnectionString**允许你在远程服务器已更改的情况下调整远程数据源。 提供 ConnectionString 时必须始终指定 DatasourceID。  
  
-   **文件夹**允许重新映射到本地硬盘上的分区的文件夹  
  
-   **原始**为本地分区的原始文件夹。  
  
-   **新**是本地分区用于驻留在相应的原始旧文件夹中的新位置。  
  
-   **密码**，如果非空，指定服务器将加密备份文件。  
  
##  <a name="Traces"></a> 跟踪对象  
 跟踪是用于监视、重播和管理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的框架。 客户端应用程序（如 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]）订阅跟踪，服务器发回跟踪定义中指定的跟踪事件。  
  
 每个事件都由事件类来描述。 事件类描述所生成事件的类型。 在事件类中，事件子类描述更细一层分类。 每个事件都由多个列来描述。 描述跟踪事件的各列对于所有事件都是一致的且符合 SQL 跟踪结构。 每列中记录的信息可能会因事件类而异；即为每个跟踪定义一组预定义的列，但列的含义可能会因事件类而异。 例如，TextData 列用于记录所有语句事件的原始 ASSL。  
  
 跟踪定义可包含一个或多个要并发跟踪的事件类。 对于每个事件类，可以将一个或多个数据列添加到跟踪定义中，但不是所有跟踪列都必须使用。 数据库管理员可以决定哪些可用列要包括在跟踪中。 此外，可以根据跟踪中任意列的筛选条件有选择地跟踪事件类。  
  
 可以启动和删除跟踪。 可以在任何同一时间运行多个跟踪。 可以实时捕获跟踪事件或者将其定向到某个文件供以后分析或重播。 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 是用于分析和重播 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 跟踪事件的工具。 允许多个连接从同一个跟踪接收事件。  
  
 跟踪可以分为两组：服务器跟踪和会话跟踪。 服务器跟踪将通知服务器中的所有事件；会话跟踪仅通知当前会话中的事件。  
  
 服务器的跟踪集合中的跟踪的定义方法如下：  
  
1.  创建 <xref:Microsoft.AnalysisServices.Trace> 对象并填充基本数据，包括跟踪 ID、名称、日志文件名、追加|覆盖等。  
  
2.  将要监视的事件添加到跟踪对象的事件集合中。 对于每个事件，添加数据列。  
  
3.  通过将筛选器添加到筛选器集合来设置筛选器，以排除不需要的数据行。  
  
4.  开始跟踪；创建跟踪不会开始收集数据。  
  
5.  停止跟踪。  
  
6.  通过 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 查看跟踪文件。  
  
 会话对象中的跟踪通过以下方式获得：  
  
1.  定义处理应用程序中由 SessionTrace 生成的跟踪事件的函数。 可能的事件为 OnEvent 和 Stopped。  
  
2.  将所定义的函数添加到事件处理程序中。  
  
3.  开始会话跟踪。  
  
4.  执行进程，使函数处理程序捕获事件。  
  
5.  停止会话跟踪。  
  
6.  继续执行应用程序。  
  
##  <a name="CaptureLog"></a> CaptureLog 类和 CaptureXML 属性  
 AMO 要执行的所有操作都会作为 XMLA 消息发送到服务器。 AMO 提供捕获所有这些没有 SOAP 标头的消息的方法。 有关详细信息，请参阅[简介 AMO 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)。 CaptureLog 是 AMO 中用于编写对象和操作脚本的机制；对象和操作脚本将以 XMLA 编写。  
  
 若要开始捕获 XML，CaptureXML 服务器对象属性应设置为**true**。 然后，将开始在 CaptureLog 类中捕获所有要发送到服务器的操作，不包括正在向服务器进行发送的操作。 CaptureLog 之所以被视为类，是因为它有一个 Clear 方法，该方法用于清除捕获日志。  
  
 若要读取该日志，请获取字符串集合并开始循环访问这些字符串。 此外，还可以使用服务器对象方法 ConcatenateCaptureLog 将所有日志串联到一个字符串中。 ConcatenateCaptureLog 要求有三个参数，其中两个是必需的。 必需的参数*事务*，为 Boolean 类型和*并行*，为 Boolean 类型。 如果*事务*设置为**true**，它指示 XML 批处理文件在由于而不是每个命令在单个事务视为分隔的事务将会创建。 如果*并行*设置为**true**，它指示与记录将并发执行，而不是按顺序记录批处理文件中的所有命令。  
  
##  <a name="AMO"></a> AMOException 异常类  
 可以使用 AMOException 异常类轻松地捕获应用程序中由 AMO 引发的异常。  
  
 AMO 将在发现各种不同的问题时引发异常。 下表列出了 AMO 所处理的异常的种类。 异常从 <xref:Microsoft.AnalysisServices.AmoException> 类派生。  
  
|异常|来源|Description|  
|---------------|------------|-----------------|  
|<xref:Microsoft.AnalysisServices.AmoException>|基类|缺少必需的父对象或者在集合中找不到请求的项时，应用程序会收到此异常。|  
|<xref:Microsoft.AnalysisServices.OutOfSyncException>|派生自 AMOException|AMO 与引擎不同步且引擎返回 AMO 不能识别的对象引用时，应用程序会收到此异常。|  
|<xref:Microsoft.AnalysisServices.OperationException>|派生自 AMOException|这是应用程序经常会收到的一个重要异常。 此异常包含来自服务器的错误的详细信息，可能是源于错误的 AMO 操作，如 Update、Process 或 Drop。|  
|<xref:Microsoft.AnalysisServices.ResponseFormatException>|派生自 AMOException|引擎返回的消息使用了 AMO 不能识别的格式时，会发生此异常。|  
|<xref:Microsoft.AnalysisServices.ConnectionException>|派生自 AMOException|如果无法建立连接（与 Server.Connect）或当 AMO 正在与引擎进行通信（例如在执行 Update、Process 或 Drop 的过程中）时连接中断，则会发生此异常。|  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices>   
 [引入 AMO 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [逻辑体系结构 & #40;Analysis Services-多维数据 & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [数据库对象 & #40;Analysis Services-多维数据 & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
