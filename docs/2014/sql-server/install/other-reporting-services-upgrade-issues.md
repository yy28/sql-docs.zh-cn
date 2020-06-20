---
title: 其他 Reporting Services 升级问题 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- command line setup [Reporting Services]
- Setup commands [Reporting Services]
- multivalued parameters [Reporting Services]
- WMI provider [Reporting Services]
- compile errors [Reporting Services]
- single-valued parameters [Reporting Services]
- data processing extensions [Reporting Services]
- report compilation errors [Reporting Services]
- authentication [Reporting Services]
ms.assetid: 42dd2f06-1de9-449e-ab9d-f4ef25f8b728
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7cba24007534f143e6b8fd4b7cf74357bbfba3a1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065314"
---
# <a name="other-reporting-services-upgrade-issues"></a>其他 Reporting Services 升级问题
  本主题介绍在升级 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能时可能会遇到的已知问题。 **升级顾问不会检测到这些问题。** 有关其他信息，请参阅[SQL Server 2014 发行说明](https://go.microsoft.com/fwlink/?LinkID=296445)  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
|问题|说明|适用于|  
|-----------|-----------------|----------------|  
|SharePoint 场升级|仅在场中的所有其他 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件已升级到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 后，才升级 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 共享服务。<br /><br /> 若要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在多节点 sharepoint 场中升级到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 必须先将场中用于 sharepoint 的外接程序的所有实例升级到该 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 版本，然后再升级 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共享服务。<br /><br /> 当 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 共享服务已升级到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 但是场中的其他 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件仍为版本 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 时，报表呈现将失败。<br /><br /> <br /><br /> 有关详细信息，请参阅 [SQL Server 2014 Reporting Services 提示、技巧和故障排除](https://go.microsoft.com/fwlink/?LinkID=391254)。|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|  
|并行安装|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]本机模式不能与以下任一项并行运行：<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]用于 SharePoint 的外接程序<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 共享服务<br /><br /> <br /><br /> 并行安装会阻止 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式 Windows 服务启动。 在 Windows 事件日志中将看到类似以下的错误消息：<br /><br /> 说明：报表服务器数据库版本无效。<br /><br /> 说明：报表服务器 [服务器名称] 无法连接到报表服务器数据库。|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 本机模式|  
|在修复失败的升级的过程中出错|**问题：** 升级失败后，尝试运行修复。 修复操作同样失败，并且您在安装日志文件中看到类似于下面的消息：<br /><br /> `(01) 2011-10-27 12:23:15 Slp:` <br /> `(01) 2011-10-27 12:23:15 Slp: Exception type: System.Exception` <br /> `(01) 2011-10-27 12:23:15 Slp:     Message:`  <br /> `(01) 2011-10-27 12:23:15 Slp:         SQLPath element is missing` <br /> `(01) 2011-10-27 12:23:15 Slp:     Data:`  <br /> `(01) 2011-10-27 12:23:15 Slp:       SQL.Setup.FailureCategory = ConfigurationFailure`<br /><br /> 有关日志文件的详细信息，请参阅[查看和读取 SQL Server 安装日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。<br /><br /> **解决方案：** 你需要卸载 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 并重新安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 无法再进行升级。|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|  
|只为最后一个请求保存交互信息。|在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的先前版本中，快照保存了所有可能的交互选择组合，例如钻取信息和切换选择。 例如，您本来可以查看报表的第五页，但通过跟踪切换的正确 ID，以编程方式切换到第一页中的项。<br /><br /> 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中，仅为最后一个呈现请求生成和保存交互信息。 您不能先查看某一页，然后以编程方式切换到另一页中的项。 只能切换当前报表页上的钻取项。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|呈现和分页方式已更改。|呈现对象模型（ROM）在中已更改 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 不再支持早期版本的呈现对象模型。 不支持从多线程呈现扩展插件中访问呈现对象模型（以及从多个线程切换上下文）。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|重新设计的 CSV 导出格式。|在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的早期版本中，当将报表导出为 CSV 文件格式时，数据格式保留为报表页上出现的数据格式。 对于矩阵数据区域，这会导致数据格式不便于导入到其他应用程序中。<br /><br /> 在此版本中，当将报表导出为 CSV 文件时，可以在两种支持的格式之间进行选择：“默认”模式和“兼容”模式。 默认模式针对 Excel 进行了优化。 兼容模式针对第三方应用程序进行了优化。<br /><br /> 不再使用 CSV 文件的早期格式。 但是，对于不使用矩阵数据区域的报表，可以使用兼容模式获得最接近于早期 CSV 文件格式的文件格式。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|页眉和页脚中带有条件可见性的聚合。|在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的早期版本中，不同呈现器使用不同的规则来确定应将哪些带有条件可见性的项包含在报表页中。 例如，不对打印报表中的隐藏项执行聚合计算，但是对使用浏览器或在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 中查看的报表中的隐藏项执行聚合计算。<br /><br /> 在此版本中，所有呈现器均使用相同的规则集来确定应将哪些项包含在页中。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|取消了对 Excel 公式的任何支持。|在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的早期版本中，为将 RDL 表达式转换为 Excel 公式提供了有限的支持。 在此版本中，当将报表导出到 Excel 时，RDL 表达式不会转换为 Excel 公式。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|重叠项。|在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的早期版本中，如果报表在报表设计图面上有重叠项，则发布报表时会生成一条警告（“并非所有呈现器都支持重叠的报表项。”），但是报表项仍然保留在设计图面中的原始位置。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中，当查看报表或将报表导出到不支持重叠项的呈现器中时，会将报表项移动到正确的重叠边界。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|报表对象模型命名空间更改。|在中 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，报表对象模型命名空间已发生更改。 此命名空间提供从自定义代码到类似 `Fields`、`Parameters` 和 `ReportItems` 的全局集合的只读访问。 如果现有自定义代码显式使用对早期命名空间的完全限定引用，则此更改是一项重大更改。<br /><br /> 建议不要使用完全限定引用来从代码访问内置集合。 通过非显式指定命名空间，自定义代码引用可解析为当前安装的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本的报表对象模型版本。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|不支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 中的报表服务器 Windows Management Instrumentation (WMI) 提供程序。|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包括一个 WMI 提供程序，用于以编程方式配置报表服务器的运行环境。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本包括一个完全替代先前版本的全新版本的 WMI 提供程序。 此版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 和 2005 版本。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|在升级后的报表服务器上不会重新创建服务主体名称 (SPN)。|如果为报表服务器 Web 服务创建了 SPN，请验证约束委派是否仍可用于升级后的报表服务器。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
|自定义程序集必须手动移到新的安装文件夹中。|自定义程序集未由升级顾问检测到；如果您想要继续在报表中使用自定义功能，这些自定义程序集必须手动移到新的安装文件夹。<br /><br /> 如果在报表服务器安装文件夹中安装这些程序集，它们需要在升级完成后移到新的安装文件夹。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP2|  
  
## <a name="see-also"></a>另请参阅  
 [升级顾问 &#40;Reporting Services 升级问题&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
