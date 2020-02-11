---
title: PowerPivot BI 语义模型连接（. bism） |Microsoft Docs
ms.custom: ''
ms.date: 04/19/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 08828eec-4f8c-4f34-a145-e442f7b7031d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 846998acaa20b572760edcc67ecd24f8346a762a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66071376"
---
# <a name="powerpivot-bi-semantic-model-connection-bism"></a>PowerPivot BI 语义模型连接 (.bism)
  BI 语义模型连接 (.bism) 是可移植的连接，可在多维模式下将 Excel 或 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报表连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格模型数据库或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。 如果您熟悉 Office 数据连接 (.odc) 文件，则您会注意到定义和使用 .bism 连接文件的方式的相似性。  
  
 BI 语义模型连接是通过 SharePoint 创建和访问的。 创建 BI 语义模型连接后，您可以对库中的 BI 语义模型连接启用快速启动命令。 快速启动命令打开新的 Excel 工作簿或选项来供您编辑连接文件。 如果已安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，你还会看到用于创建 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报表的命令。  
  
 ![BISM 快速启动命令的屏幕快照](../media/ssas-bism-quicklaunch.gif "BISM 快速启动命令的屏幕快照")  
  
##  <a name="bkmk_prereq"></a>支持的数据库  
 BI 语义模型连接指向表格模型数据。 存在三种可用于此数据的数据源：  
  
-   以表格服务器模式在独立的 Analysis Services 实例上运行的表格模型数据库。 独立 Analysis Services 实例的部署位于场外部。 访问场外部的数据源要求附加权限，您可在本主题中阅读相关信息： [Create a BI Semantic Model Connection to a Tabular Model Database](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)。  
  
-   保存到 SharePoint 的 PowerPivot 工作簿。 Excel 工作簿内嵌入的 PowerPivot 数据库等效于在独立的 Analysis Services 表格模式服务器上运行的表格模型数据库。 如果您已经使用 PowerPivot for Excel 和 PowerPivot for SharePoint，则可以定义指向 SharePoint 库中 PowerPivot 工作簿的 BI 语义模型连接，并且使用现有 PowerPivot 数据生成 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报表。  您可以使用在 PowerPivot for Excel 的 SQL Server 2008 R2 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本中创建的工作簿。  
  
-   
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的多维数据模型。  
  
 有关数据源的比较，请参阅社区内容[了解 SQL Server 2012 BI 语义模型（BISM）](http://www.mssqltips.com/sqlservertip/2818/understanding-the-sql-server-2012-bi-semantic-model-bism/)。  
  
## <a name="understanding-the-connection-sequence-for-bi-semantic-connections"></a>理解 BI 语义连接的连接顺序  
 本节介绍不同客户端应用程序（例如 Excel 桌面应用程序或 SharePoint 上的 Power View 报表客户端）与 SharePoint 场内部或外部的表格模型数据库之间的连接行为。  
  
 与表格模型数据库的所有连接都是使用正请求数据的用户的凭据建立的。 但是，该连接的机制将受到以下因素的影响：连接是否为场内连接、是单跃点还是双跃点连接以及是否启用了 Kerberos。 有关 SharePoint 和后端数据源之间经身份验证的连接的详细信息，请参阅 [双跃点身份验证：NTLM 为什么失败以及 Kerberos 为什么有效](https://go.microsoft.com/fwlink/?LinkId=237137)。  
  
 **从 Excel 连接到网络上的表格数据**  
  
 在某个 Excel 用户将 BI 语义模型连接指定为数据源时，.bism 文件中的连接信息将下载到客户端应用程序，然后将它自己的直接请求发布到 Analysis Services 上的表格模型数据库。 若要访问该 .bism 连接，此 Excel 用户必须是对该 .bism 连接文件具有读取权限的 SharePoint 用户。 在下载了连接信息后，所有后续连接都将绕过 SharePoint，直接从 Excel 流到后端表格模型数据库。  
  
 下图说明此连接顺序。 它从针对此 .bism 连接的请求开始，随后是将连接信息下载到客户端，最后是与数据库的单跃点连接。 该连接是使用对 Analysis Services 数据库具有读取权限的 Excel 用户的 Windows 凭据建立的。 该连接是单跃点连接；因此，即使启用了 Kerberos，在此环境下也不需要 Kerberos。  
  
 ![从 Excel 连接到表格模型数据库](../media/ssas-powerpivotbismconnection-1.gif "从 Excel 连接到表格模型数据库")  
  
 **从 Power View 连接到网络上的表格数据**  
  
 在某一 SharePoint 用户在文档库中单击某一 BI 语义连接后，Power View（如果已安装）将立即启动并且打开与表格模型数据库的连接。  
  
 Power View 和表格模型数据库之间的连接遵循双跃点身份验证顺序，其中，用户标识从客户端流到 SharePoint，然后从 SharePoint 流到在场外运行的后端 Analysis Services 表格模型数据库。 处理连接请求的 ADOMD.NET 客户端库在首次尝试时始终会尝试使用 Kerberos。 如果配置了 Kerberos，则在与表格模型数据库的连接上将模拟该用户标识，并且连接将成功。  
  
 如果未配置 Kerberos 并且请求失败，则 Reporting Services 将进行第二次尝试。 在这种情况下，客户端库将使用 Reporting Services 服务标识和 NTLM 身份验证连接到 Analysis Services。 Power View 用户的标识使用 `effectiveusername` 参数传递到连接字符串上。  
  
 在 Analysis Services 实例上，只有系统管理员角色的成员才有权使用 `effectiveusername` 参数进行连接和模拟该服务器实例上的其他用户。 因此，Reporting Services 共享服务的执行帐户必须对 Analysis Services 实例具有管理权限。  主题 [创建与表格模型数据库的 BI 语义模型连接](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)中将提供有关向服务帐户授予管理权限的说明。  
  
 下图展示了将相同 Windows 用户标识用于每个连接的连接顺序。 在与 Analysis Services 的最后连接上，按 Reporting Services 服务应用程序标识进行连接，并且使用 `effectiveusername` 传递 Windows 用户标识。  
  
 ![到表格数据库的模拟连接](../media/ssas-powerpivotbismconnection-2.gif "到表格数据库的模拟连接")  
  
 **从 Power View 连接到 SharePoint 中的 PowerPivot 数据**  
  
 在某一 SharePoint 用户单击解析为相同场中的 PowerPivot 工作簿的某一 BI 语义连接后，连接将在 SharePoint 环境的上下文内发生。 PowerPivot 服务应用程序将处理连接请求，将其转发到同一计算机上的 Analysis Services 实例。 该 Analysis Services 实例将从工作簿中提取 PowerPivot 数据并且加载这些数据。 所有后续连接均由场中的 PowerPivot 服务应用程序进行管理。  
  
 在这种情况下，所有连接都在同一个场中发生，因此，没有对 Kerberos 或约束委托的要求。  
  
##  <a name="bkmk_rel"></a> 相关任务  
 [将 BI 语义模型连接内容类型添加到库 &#40;PowerPivot for SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md)  
  
 [创建与 PowerPivot 工作簿的 BI 语义模型连接](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
 [Create a BI Semantic Model Connection to a Tabular Model Database](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
 [在 Excel 或 Reporting Services 中使用 BI 语义模型连接](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [确定 Analysis Services 实例的服务器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [连接到 Analysis Services](../instances/connect-to-analysis-services.md)  
  
  
