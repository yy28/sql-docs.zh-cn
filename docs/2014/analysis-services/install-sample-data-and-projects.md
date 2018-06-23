---
title: 安装适用于 Analysis Services 多维建模教程 Sample Data and Projects |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fc475b25-cbb2-408a-901f-9299299538c5
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: 2d1aca34ac45c88452b83444c7287595c22bb453
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027104"
---
# <a name="install-sample-data-and-projects-for-the-analysis-services-multidimensional-modeling-tutorial"></a>安装 Analysis Services 多维建模教程的示例数据和项目
  可使用本主题中提供的说明和链接来安装 Analysis Services 教程中使用的所有数据和项目文件。  
  
## <a name="step-1-install-sql-server-software"></a>步骤 1：安装 SQL Server 软件  
 本教程中的课程假定您已安装以下软件。 所有以下软件都使用 SQL Server 安装介质进行安装。 为了简化部署，您可以在一台计算机上安装所有功能。 若要安装这些功能，请运行 SQL Server 安装程序并从“功能选择”页中选择它们。 有关详细信息，请参阅[从安装向导安装 SQL Server 2014&#40;安装&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。  
  
-   数据库引擎  
  
-   Analysis Services  
  
     Analysis Services 仅在以下版本中提供：Evaluation、Enterprise、Business Intelligence、Standard。  
  
     请注意，SQL Server Express 版本不包括 Analysis Services。 如果要免费试用此软件，[请下载 Evaluation Edition](http://go.microsoft.com/fwlink/?LinkId=392824) 。  
  
     默认情况下，Analysis Services 将作为多维实例安装，您可以通过在安装向导的“服务器配置”页中选择“表格服务器模式”来覆盖此实例。 如果要同时运行两种服务器模式，请在同一台计算机上重新运行 SQL Server 安装程序，以在另一模式中再安装一个 Analysis Services 实例。  
  
-   SQL Server Management Studio  
  
 或者，请考虑安装 Excel 以便在您继续执行本教程时浏览您的多维数据。 通过安装 Excel，可以启用“在 Excel 中分析”功能。该功能可以使用连接到你要生成的多维数据集的数据透视表字段列表来启动 Excel。 建议使用 Excel 来浏览数据，因为您可以快速生成透视报表，并通过它与数据进行交互。  
  
 或者，您可以使用在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中内置的内置 MDX 查询设计器来浏览数据。 查询设计器将返回相同的数据，除非数据以平面行集的形式表示。  
  
## <a name="step-2-download-sql-server-data-tools--business-intelligence-for-visual-studio-2012"></a>步骤 2：下载 SQL Server Data Tools - Business Intelligence for Visual Studio 2012  
 在此版本中，SQL Server Data Tools 和其他 SQL Server 功能将分开下载与安装。 用于创建 BI 模型和报表的设计器与项目模板现在作为免费 Web 下载提供。  
  
-   [下载 SQL Server Data Tools 的 Business Intelligence 版本](http://go.microsoft.com/fwlink/p/?LinkID=322038)。 文件将保存到 Downloads 文件夹。 运行安装程序以安装此工具。  
  
     重新启动计算机以完成安装。  
  
## <a name="step-3-install-databases"></a>步骤 3：安装数据库  
 Analysis Services 多维模型使用您从关系数据库管理系统导入的事务数据。 为了实现本教程教学目的，您将使用以下关系数据库作为数据源。  
  
-   **AdventureWorksDW2012** – 这是一个在数据库引擎实例上运行的关系数据仓库。 它提供了将由您在本教程中生成和部署的 Analysis Services 数据库和项目使用的原始数据。  
  
     您可以将此示例数据库与 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 和 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]一起使用。  
  
 若要安装此数据库，请执行以下操作：  
  
1.  从 codeplex 上的产品示例页下载 [AdventureWorkDW2012](http://go.microsoft.com/fwlink/p/?LinkID=221770) 数据库。  
  
     数据库文件名称是 AdvntureWorksDW2012_Data.mdf。 该文件应位于您的计算机上的 Downloads 文件夹中。  
  
2.  将 AdventureWorksDW2012_Data.mdf 文件复制到本地 SQL Server 数据库引擎实例的数据目录。 默认情况下，该文件位于 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data。  
  
3.  启动 SQL Server Management Studio 并连接到数据库引擎实例。  
  
4.  右键单击“数据库”，然后单击“附加”。  
  
5.  单击 **“添加”**。  
  
6.  选择 **AdventureWorksDW2012_Data.mdf** 数据库文件，并单击“确定”。 如果未列出该文件，请检查 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data 文件夹，以便确保该文件在该路径下存在。  
  
7.  在数据库详细信息中，删除日志文件条目。 安装程序假设您具有日志文件，但在示例中没有日志文件。 附加数据库时将自动创建新日志文件。 选择日志文件并单击“删除”，然后单击“确定”以只附加主数据库文件。  
  
## <a name="step-4-grant-database-permissions"></a>步骤 4：授予数据库权限  
 示例项目使用数据源模拟设置，这些设置可指定导入或处理数据所用的安全上下文。 默认情况下，模拟设置指定用于访问数据的 Analysis Services 服务帐户。 若要使用此默认设置，必须确保 Analysis Services 运行时使用的服务帐户具有对 **AdventureWorksDW2012** 数据库的数据读取器权限。  
  
> [!NOTE]  
>  出于学习的目的，建议您在 SQL Server 中使用默认服务帐户模拟选项并向服务帐户授予数据读取器权限。 尽管提供了其他模拟选项，但并非所有这些选项都适用于处理操作。 具体而言，使用当前用户的凭据的选项不支持处理操作。  
  
1.  确定服务帐户。 您可以使用 SQL Server 配置管理器或“服务”控制台应用程序来查看帐户信息。 如果使用默认帐户将 Analysis Services 作为默认实例安装，则该服务将作为 **NT Service\MSSQLServerOLAPService**运行。  
  
2.  在 Management Studio 中，连接到数据库引擎实例。  
  
3.  展开“安全性”文件夹，右键单击“登录名”，然后选择“新建登录名”。  
  
4.  在“常规”页的“登录名”中，键入 **NT Service\MSSQLServerOLAPService**（或运行该服务所用的任何帐户）。  
  
5.  单击“用户映射”。  
  
6.  选中 **AdventureWorksDW2012** 数据库旁边的复选框。 角色成员身份应自动包括 **db_datareader** 和 **public**。 单击“确定”接受默认值。  
  
## <a name="step-5-install-projects"></a>步骤 5：安装项目  
 教程包括一些示例项目，以便您能将您的结果与完成的项目进行比较，或者学习后面的课程。  
  
 第 4 课的项目文件特别重要，因为它不仅为第 4 课而且还为所有后续课程提供了基础。 在之前的项目文件中，按照教程中的步骤操作可得到与完成的项目文件完全一样的副本，而第 4 课的示例项目与此有很大的不同，它包含了在第 1 课到第 3 课中生成的模型中没有的、新的模型信息。 第 4 课假定您是下面的下载链接提供的示例项目文件的初学者。  
  
1.  在 codeplex 上的产品示例页中下载 [Analysis Services 教程 SQL Server 2012](http://go.microsoft.com/fwlink/p/?LinkID=221866) 。  
  
     2012 教程对于 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本有效。  
  
     “Analysis Services Tutorial SQL Server 2012.zip”文件将保存到您的计算机上的 Downloads 文件夹中。  
  
2.  将 .zip 文件移到根驱动器下一级的文件夹（例如 C:\Tutorial）。 如果您尝试在 Downloads 文件夹中解压缩这些文件，则此步骤将会缓解有时候会发生的“路径过长”错误。  
  
3.  解压缩示例项目：右键单击该文件，然后选择“全部提取”。 提取这些文件后，您应该已在计算机上安装以下项目：  
  
    -   Lesson 1 Complete  
  
    -   Lesson 2 Complete  
  
    -   Lesson 3 Complete  
  
    -   Lesson 4 Complete  
  
    -   Lesson 4 Start  
  
    -   Lesson 5 Complete  
  
    -   Lesson 6 Complete  
  
    -   Lesson 7 Complete  
  
    -   Lesson 8 Complete  
  
    -   Lesson 9 Complete  
  
    -   Lesson 10 Complete  
  
4.  取消对这些文件的只读权限。 右键单击父文件夹“Analysis Services Tutorial SQL Server 2012”，选择“属性”，然后清除“只读”复选框。 单击“确定” 。 将更改应用至此文件夹、子文件夹和文件。  
  
5.  启动 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
6.  打开与您要使用的课程对应的解决方案 (.sln) 文件。 例如，在名为“Lesson 1 Complete”的文件夹中，您应打开 Analysis Services Tutorial.sln 文件。  
  
7.  部署解决方案以验证是否正确设置了数据库权限和服务器位置信息。  
  
     如果 Analysis Services 和数据库引擎是作为默认实例 (MSSQLServer) 安装的，并且所有软件在同一台计算机上运行，则可以单击“生成”菜单上的“部署解决方案”来生成示例项目并将其部署到本地 Analysis Services 实例。 在部署过程中，将从本地数据库引擎实例上的 **AdventureWorksDW2012** 数据库处理（或导入）数据。 将在包含从数据库引擎检索的数据的 Analysis Services 实例上创建新的 Analysis Services 数据库。  
  
     如果出现错误，请检查前面关于设置数据库权限的步骤。 此外，您还可能需要更改服务器名称。 默认服务器名称为 localhost。 如果服务器安装在远程计算机上或作为命名实例安装，必须覆盖默认名称以使用对于您的安装有效的服务器名称。 此外，如果服务器位于远程计算机上，则可能需要配置 Windows 防火墙以允许对它们进行访问。  
  
     用于连接到数据库引擎的服务器名称在多维解决方案的数据源对象中指定（《Adventure Works 教程》），并在解决方案资源管理器中可见。  
  
     用于连接到 Analysis Services 的服务器名称在项目“属性页”的“部署”选项卡中指定，并且也在解决方案资源管理器中可见。  
  
8.  启动 SQL Server Management Studio。 在 SQL Server Management Studio 中，连接到 Analysis Services。 验证名为 **Analysis Services Tutorial** 的数据库是否正在服务器上运行。  
  
## <a name="next-step"></a>下一步  
 您现在可以使用本教程了。 有关如何入门的详细信息，请参阅[多维建模（Adventure Works 教程）](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)。  
  
## <a name="see-also"></a>请参阅  
 [从安装向导安装 SQL Server 2014&#40;安装程序&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)   
 [配置 Windows 防火墙以允许 Analysis Services 访问](instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)   
 [配置 Windows 防火墙以允许 SQL Server 访问](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  