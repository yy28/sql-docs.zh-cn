---
title: 工具和 Analysis Services 中使用的应用程序 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8d3ecb5de4c70c09bc367b9008f5d62c6a23faef
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210065"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>在 Analysis Services 中使用的工具和应用程序
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  查找工具和应用程序都需要为生成 Analysis Services 模型和管理已部署的数据库。  
  
## <a name="analysis-services-model-designers"></a>Analysis Services 模型设计器  
 使用项目模板在 SQL Server Data Tools (SSDT)，Visual Studio shell 创作模型。 项目模板提供用于创建包含 Analysis Services 解决方案的数据模型对象的模型设计器。 SSDT 是每月更新一个免费 web 下载。

 **[下载 SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)** 
  
 模型具有兼容性级别设置，可确定功能的可用性和哪个版本的 Analysis Services 运行模型。  是否可以指定给定兼容性级别确定部分由模型设计器。  
  
 表格模型使用最新功能，如 BIM 文件以表格的 JSON 格式和的双向交叉筛选，必须创建或升级兼容性级别为 1200年或更高版本。  
  
 如果需要较低的兼容性级别，可能是因为你想要部署的 Analysis Services 的早期版本上的模型仍可在模型设计器在 SSDT 中。 较新版本的工具支持在任何兼容性级别创建所有模型类型 （表格或多维）。   

## <a name="administrative-tools"></a>管理工具  
  
 SQL Server Management Studio (SSMS) 是所有 SQL Server 功能，包括 Analysis Services 的主要管理工具。 SSMS 是免费 web 下载每月更新。 
  
**[下载 SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)** 
  
 SSMS 包括扩展的事件 (xEvents)，提供用于监视活动和诊断问题 SQL Server 2016 和 Azure Analysis Services 服务器上的 SQL Server Profiler 跟踪的轻量替代。 若要了解更多信息，请参阅 [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) 。  
  
### <a name="sql-server-profiler"></a>SQL Server 事件探查器  
 SQL Server Profiler 提供一种熟悉的方法，用以监视连接、MDX 查询执行和其他服务器操作，但就官方而言，从 xEvents 角度出发不推荐使用此方法。 SQL Server Profiler 将按默认安装。 您可以找到它与 SQL Server 上应用的应用程序在 Windows 中。  
  
### <a name="powershell"></a>PowerShell  
 可以使用 PowerShell 命令执行许多管理任务。 请参阅[PowerShell 参考](../analysis-services/powershell/analysis-services-powershell-reference.md)有关详细信息。  
  
### <a name="community-and-third-party-tools"></a>社区和第三方工具  
 检查 [Analysis Services codeplex 页面](http://sqlsrvanalysissrvcs.codeplex.com/) 是否具有社区代码示例。 当寻求对支持 Analysis Services 的第三方工具的推荐时，可在[论坛](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) 获得帮助。  
  
## <a name="see-also"></a>请参阅  
 [多维数据库的兼容性级别](../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [表格模型的兼容性级别](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
