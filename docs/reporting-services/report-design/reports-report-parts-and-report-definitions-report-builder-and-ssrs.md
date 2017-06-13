---
title: "报表，报表部件，和报表定义 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report definitions
- reports
ms.assetid: 2d746550-f8cc-4e97-8a06-d0f03cffc18d
caps.latest.revision: 26
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3c5a2673c5e38d6bd216116cd14225f1ed064487
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="reports-report-parts-and-report-definitions-report-builder-and-ssrs"></a>报表、报表部件和报表定义（报表生成器和 SSRS）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用各种术语来描述不同状态的分页报表，包括初始定义、发布的报表以及显示给用户查看的报表。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-definition-rdl-files"></a>报表定义 (.rdl) 文件  
 报表定义是一种在报表生成器或报表设计器中创建的文件。 对于数据源连接、用来检索数据的查询、表达式、参数、图像、文本框、表以及可能包含在报表中的任何其他设计时元素，它都提供了完整的说明。 尽管报表定义可以很复杂，但是也可以在最低条件下只指定一个查询以及其他报表内容、报表属性和报表布局。  
  
 在运行时，报表定义作为已处理的报表呈现。 此时，将从数据源检索数据并根据报表定义中的说明设置数据格式。 可以从计算机直接运行报表定义并将其保存到本地，也可以将报表定义发布到报表服务器，以便其他人也可以运行报表定义。  
  
 报表定义以 XML 格式编写，该格式应符合一种称为报表定义语言 (RDL) 的 XML 语法。 RDL 描述了 XML 元素，包括报表会采用的所有可能变体。  
  
## <a name="client-report-definition-rdlc-files"></a>客户端报表定义 (.rdlc) 文件  
 Visual Studio 报表设计器产生客户端报表定义 (.rdlc) 文件以供与 ReportViewer 控件结合使用。 .rdlc 文件可以转换为 .rdl 文件以供与 Reporting Services 报表设计器结合使用。  
  
## <a name="report-part-rsc-files"></a>报表部件 (.rsc) 文件  
 报表部件是自包含的报表项，存储在报表服务器上并可以包含在其他报表中。 使用报表生成器可以从报表部件库中浏览和选择部件，以添加到报表中。 使用报表设计器或报表生成器可以将报表部件保存在报表部件库中以供使用。  
  
 报表部件定义是报表定义文件的 XML 片段。 您可以通过创建报表定义，然后选择报表中要单独发布为报表部件的报表项，从而创建报表部件。 报表部件包括数据区域、矩形及其包含项以及图像。 您可以保存报表部件及其相关数据集和共享数据源参考，这样它就可以在其他报表中重新使用。  
  
 有关详细信息，请参阅[报表部件（报表生成器和 SSRS）](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)和[报表设计器中的报表部件 (SSRS)](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)。  
  
## <a name="published-reports"></a>发布的报表  
 创建 .rdl 文件后，可以将其保存到本地，也可以将其保存到报表服务器上的个人文件夹（如“我的报表”文件夹）。 报表准备就绪可供他人查看时，可通过从报表生成器中将其保存到报表服务器上的公共文件夹，通过 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 门户上传它，或者从报表设计器中部署报表项目解决方案，从而发布此报表。 发布的报表存储在报表服务器数据库中，并在报表服务器或 SharePoint 站点上进行管理。  
  
 发布的报表是通过角色分配进行保护的，这种角色分配使用的是基于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 角色的安全模式。 通过 URL、SharePoint Web 部件或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 门户，即可访问发布的报表，也可以导航到发布的报表并在报表生成器中打开这些报表。  
  
### <a name="report-snapshots"></a>报表快照  
 报表也可以作为包含自报表最初运行时起的布局信息和数据的快照进行发布。 报表快照不以特定的呈现格式进行保存。 相反，将以用户或应用程序发出请求时的最终查看格式（如 HTML）来呈现报表快照。 有关详细信息，请参阅[在报表管理器中查找和查看报表（报表生成器和 SSRS）](https://msdn.microsoft.com/library/dd255286.aspx)。  
  
## <a name="rendered-reports"></a>呈现的报表  
 呈现的报表是经过完全处理的报表，其中包含格式适于查看（例如 HTML）的数据和布局信息。 只有在报表以输出格式呈现之后，才能查看报表。 您可以通过执行以下操作之一来呈现报表：  
  
-   在报表生成器或报表设计器中创建或打开报表并运行该报表。  
  
-   在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 门户中查找某个报表并运行该报表。  
  
-   在与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器集成的 SharePoint 站点上查找并运行报表。  
  
-   订阅报表，这样报表将以您指定的输出格式传递到电子邮件收件箱或文件共享位置。  
  
 订阅报表，这样报表将以您指定的输出格式传递到电子邮件收件箱或文件共享位置。 报表的默认呈现格式为 HTML 4.0。 除了 HTML 之外，报表还可以用多种输出格式呈现，其中包括 Excel、Word、XML、PDF、TIFF 和 CSV。 与发布的报表一样，无法编辑呈现的报表，也不能将其保存回报表服务器。 有关详细信息，请参阅 [导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [报表创作概念（报表生成器和 SSRS）](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [SQL Server 2016 中的报表生成器](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [查找、查看和管理报表（报表生成器和 SSRS）](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
