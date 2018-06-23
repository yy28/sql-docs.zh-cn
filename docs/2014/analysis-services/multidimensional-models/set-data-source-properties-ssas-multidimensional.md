---
title: 设置数据源属性 (SSAS 多维) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.sqlserverstudio.datasourceproperties.f1
helpviewer_keywords:
- Data Source Properties dialog box
ms.assetid: bf8b600f-5b99-4f7d-908b-8a391721e9dd
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fdd8eca5f49e79c3f6d284a404f23121a1182a0f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018305"
---
# <a name="set-data-source-properties-ssas-multidimensional"></a>设置数据源属性（SSAS 多维）
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，数据源对象指定与向多维模型提供数据的外部数据仓库或关系数据库的连接。 针对数据源的属性确定连接字符串、超时间隔、连接的最大数目以及事务隔离级别。  
  
## <a name="set-data-source-properties-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中设置数据源属性  
  
1.  在解决方案资源管理器中双击某一数据源以便打开数据源设计器。  
  
2.  在数据源设计器中单击 **“模拟信息”** 选项卡。 有关创建数据源的详细信息，请参阅[创建数据源&#40;SSAS 多维&#41;](create-a-data-source-ssas-multidimensional.md)。  
  
## <a name="set-data-source-properties-in-management-studio"></a>在 Management Studio 中设置数据源属性  
  
1.  展开数据库文件夹，打开数据库名称下的“数据源”文件夹，在“对象资源管理器”中右键单击某一数据源，然后选择“属性”。  
  
2.  （可选）修改名称、说明或模拟选项。 有关详细信息，请参阅[设置模拟选项（SSAS - 多维）](set-impersonation-options-ssas-multidimensional.md)。  
  
## <a name="data-source-properties"></a>数据源属性  
  
|术语|定义|  
|----------|----------------|  
|**名称、ID、说明**|名称、ID 和说明用于标识和描述多维模型中的数据源对象。<br /><br /> 名称和说明可在您部署或处理解决方案后在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中指定。<br /><br /> ID 在创建对象时生成。 尽管您可以轻松地修改名称和说明，但 ID 是只读的并且不应更改。 一个固定的对象 ID 可在整个模型中保持对象的依赖关系和引用。|  
|**创建时间戳**|该只读属性出现在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中。 它显示数据源的创建日期和时间。|  
|**上次架构更新时间**|该只读属性出现在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中。 它显示上次更新数据源元数据的日期和时间。 当您部署解决方案时将更新此值。|  
|**查询超时值**|指定对于连接请求在尝试多长时间后将放弃连接请求。<br /><br /> 按以下格式键入查询超时值:<br /><br /> *\<小时 >*:*\<分钟 >*:*\<秒 >*<br /><br /> 此属性可由`DatabaseConnectionPoolTimeoutConnection`服务器属性。 如果该服务器属性更小，将使用该属性而非 **“查询超时值”**。<br /><br /> 有关详细信息**查询超时值**属性，请参阅<xref:Microsoft.AnalysisServices.DataSource.Timeout%2A>。 有关服务器属性的详细信息，请参阅 [OLAP Properties](../server-properties/olap-properties.md)。|  
|**连接字符串**|指定向多维模型提供数据的数据库的物理位置以及用于连接的数据访问接口。 将向生成连接请求的客户端库提供此信息。 访问接口确定可对连接字符串设置哪些属性。<br /><br /> 使用您在 **“连接管理器”** 对话框中提供的信息来生成连接字符串。 您还可以在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的数据源属性页中查看和编辑该连接字符串。<br /><br /> 对于 SQL Server 数据库中，连接字符串，包含`user ID`指示数据库身份验证; 连接包含`Integrated Security=SSPI`指示 Windows 身份验证。<br /><br /> 如果数据库被移到了一个新位置，则您可以更改服务器或数据库名称。 请确保验证当前为连接指定的凭据映射到某一数据库登录名。|  
|**最大连接数**|指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接到数据源所允许的最大连接数。 如果需要更多的连接，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将在连接可用前等待。 默认值为 10。 限制连接数目可确保不会因 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 请求而导致外部数据源重载。|  
|**隔离**|指定与关系数据库的连接发出的 SQL 命令的锁定和行版本控制行为。 有效值为 ReadCommitted 或 Snapshot。 默认值是 ReadCommitted，它指定必须在读取数据前提交数据，从而防止脏读。 快照指定读取的内容来自以前提交的数据的快照。 有关 SQL Server 中隔离级别的详细信息，请参阅 [SET TRANSACTION ISOLATION LEVEL (Transact-SQL)](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)。|  
|**托管提供程序**|如果数据源使用托管提供程序，则显示托管提供程序的名称，例如 System.Data.SqlClient、System.Data.OracleClient。<br /><br /> 如果数据源未使用托管提供程序，则此属性显示一个空字符串。<br /><br /> 该属性在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中为只读。 若要更改对连接使用的访问接口，请编辑连接字符串。|  
|**模拟信息**|指定在连接到使用 Windows 身份验证的数据源时 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 运行所基于的 Windows 标识。 选项包含使用一组预定义的 Windows 凭据、服务帐户、当前用户的标识或者在您的模型包含多个数据源对象时可能会很有用的继承选项。 有关详细信息，请参阅[设置模拟选项（SSAS - 多维）](set-impersonation-options-ssas-multidimensional.md)。<br /><br /> 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，有效的值列表包含以下值：<br /><br /> **ImpersonateAccount** （使用特定的 Windows 用户名和密码连接到数据源）。<br /><br /> **ImpersonateServiceAccount** （使用服务帐户的安全标识连接到数据源）。 这是默认值。<br /><br /> **ImpersonateCurrentUser** （使用当前用户的安全标识连接到数据源）。 此选项仅对于从外部数据仓库或数据库检索数据的数据挖掘查询有效；对于用于在多维数据库中进行处理、加载或写回的数据连接，不要选择此选项。<br /><br /> “继承”或“默认值”（使用包含此数据源对象的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的模拟设置）。 数据库属性包括模拟选项。|  
  
## <a name="see-also"></a>请参阅  
 [多维模型中的数据源](data-sources-in-multidimensional-models.md)   
 [创建数据源&#40;SSAS 多维&#41;](create-a-data-source-ssas-multidimensional.md)  
  
  
