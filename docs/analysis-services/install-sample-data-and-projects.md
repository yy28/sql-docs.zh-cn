---
title: 安装 Analysis Services 示例数据和项目 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df7311aad9c356376fffafc8a4882af8e29e746b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659236"
---
# <a name="install-sample-data-and-multidimensional-projects"></a>安装示例数据和多维项目 
[!INCLUDE[ssas-appliesto-sqlas-all](../includes/ssas-appliesto-sqlas-all.md)]

使用的说明和本文中提供的链接安装 Analysis Services 教程中使用的数据和项目文件。 
  
## <a name="step-1-install-prerequisites"></a>第 1 步：安装先决条件 
本教程中的课程假定您已安装以下软件。 您可以在一台计算机上安装的所有功能。 若要安装这些功能，请运行 SQL Server 安装程序并从“功能选择”页中选择它们。  
  
-   SQL Server 数据库引擎  
  
-   SQL Server Analysis Services  (SSAS) 
  
    Analysis Services 是在仅限这些版本中可用：评估版，企业版、 商业智能，标准。 Azure Analysis Services 中不支持多维模型。
  
    默认情况下，作为表格实例，您可以替代通过在服务器中的安装向导的配置页选择多维服务器模式安装 Analysis Services 2016 及更高版本。
  
## <a name="step-2-download-and-install-developer-and-management-tools"></a>第 2 步：下载并安装开发人员和管理工具
SQL Server Data Tools (SSDT) for Visual Studio 是单独下载和安装其他 SQL Server 功能。 设计器和用于创建 BI 模型和报表的项目模板包含在 SSDT 中的 Visual Studio 2015 或作为[Nuget 包](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)Visual Studio 2017。  
  
[下载 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=827542)。   

SQL Server Management Studio (SSMS) 是下载和其他 SQL Server 功能分开安装。  

[下载 SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)  

或者，请考虑安装 Excel 以便在您继续执行本教程时浏览您的多维数据。 通过安装 Excel，可以启用“在 Excel 中分析”功能。该功能可以使用连接到你要生成的多维数据集的数据透视表字段列表来启动 Excel。 建议使用 Excel 来浏览数据，因为您可以快速生成透视报表，并通过它与数据进行交互。  
  
或者，您可以使用在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中内置的内置 MDX 查询设计器来浏览数据。 查询设计器将返回相同的数据，除非数据以平面行集的形式表示。  
  
## <a name="step-3-install-databases"></a>步骤 3：安装数据库  
Analysis Services 多维模型使用您从关系数据库管理系统导入的事务数据。 出于本教程的目的，您使用以下关系数据库作为数据源。  
  
-   **AdventureWorksDW2012 或更高版本**-这是一个数据库引擎实例运行的关系数据仓库。 它提供了使用的 Analysis Services 数据库和项目的生成和部署在本教程的原始数据。 本教程假定你使用 AdventureWorksDW2012，但是，更高版本执行工作。
  
    可以使用与此示例数据库[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]及更高版本。 在常规，应使用匹配你的数据库引擎版本的示例数据库版本。
  
若要安装数据库，请执行以下操作：  
  
1.  下载[AdventureWorkDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) GitHub 中的数据库备份。  
  
2.  将备份文件复制到本地 SQL Server 数据库引擎实例的数据目录。
  
3.  启动 SQL Server Management Studio 并连接到数据库引擎实例。  
  
4.  还原数据库。  
  
## <a name="step-4-grant-database-permissions"></a>步骤 4：Grant 数据库权限  
示例项目使用数据源模拟设置，这些设置可指定导入或处理数据所用的安全上下文。 默认情况下，模拟设置指定用于访问数据的 Analysis Services 服务帐户。 若要使用此默认设置，您必须确保 Analysis Services 运行的服务帐户具有数据读取器权限**AdventureWorksDW**数据库。  
  
> [!NOTE]  
> 出于学习的目的，建议您在 SQL Server 中使用默认服务帐户模拟选项并向服务帐户授予数据读取器权限。 尽管提供了其他模拟选项，但并非所有这些选项都适用于处理操作。 具体而言，使用当前用户的凭据的选项不支持处理操作。  
  
1.  确定服务帐户。 您可以使用 SQL Server 配置管理器或“服务”控制台应用程序来查看帐户信息。 如果使用默认帐户将 Analysis Services 作为默认实例安装，则该服务将作为 **NT Service\MSSQLServerOLAPService**运行。  
  
2.  在 Management Studio 中，连接到数据库引擎实例。  
  
3.  展开“安全性”文件夹，右键单击“登录名”，然后选择“新建登录名”。  
  
4.  在“常规”页的“登录名”中，键入 **NT Service\MSSQLServerOLAPService**（或运行该服务所用的任何帐户）。  
  
5.  单击“用户映射”。  
  
6.  选中的复选框旁边**AdventureWorksDW**数据库。 角色成员身份应自动包括 **db_datareader** 和 **public**。 单击“确定”接受默认值。  
  
## <a name="step-5-install-projects"></a>步骤 5：安装项目  

教程包括一些示例项目，以便您能将您的结果与完成的项目进行比较，或者学习后面的课程。  
  
1.  下载[adventure-工作原理的多维-教程-projects.zip](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services)从 Adventure Works for GitHub 上的 Analysis Services 示例页。  
  
    教程项目适用于[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]及更高版本。  
  
2.  将 .zip 文件移到根驱动器下一级的文件夹（例如 C:\Tutorial）。 此步骤将会缓解有时如果您尝试解压缩的下载文件夹中的文件，则会发生的"路径过长"错误。  
  
3.  解压缩示例项目：右键单击该文件，然后选择“全部提取”。 提取文件后，你应该具有文件夹第 1 课 2、 3、 5、 6、 7、 8、 9、 10 完成和 Lesson 4 Start。 
  
4.  取消对这些文件的只读权限。 右键单击父文件夹中，选择**属性**，然后清除有关复选框**只读**。 单击“确定” 。 将更改应用至此文件夹、子文件夹和文件。  

5.  打开在的课程对应的解决方案 (.sln) 文件。 例如，在名为“Lesson 1 Complete”的文件夹中，您应打开 Analysis Services Tutorial.sln 文件。  
  
6.  部署解决方案以验证数据库权限和服务器位置信息安装正确。  
  
    如果 Analysis Services 和数据库引擎是作为默认实例 (MSSQLServer) 安装的，并且所有软件在同一台计算机上运行，则可以单击“生成”菜单上的“部署解决方案”来生成示例项目并将其部署到本地 Analysis Services 实例。 在部署期间，为处理 （或导入数据） 从**AdventureWorksDW**本地数据库引擎实例上的数据库。 包含从数据库引擎检索的数据的 Analysis Services 实例上创建新的 Analysis Services 数据库。  
  
    如果出现错误，请检查前面关于设置数据库权限的步骤。 此外，您还可能需要更改服务器名称。 默认服务器名称为 localhost。 如果服务器安装在远程计算机上或作为命名实例安装，必须覆盖默认名称以使用对于您的安装有效的服务器名称。 此外，如果服务器位于远程计算机上，则可能需要配置 Windows 防火墙以允许对它们进行访问。  
  
    用于连接到数据库引擎的服务器名称在多维解决方案的数据源对象中指定（《Adventure Works 教程》），并在解决方案资源管理器中可见。  
  
    用于连接到 Analysis Services 的服务器名称在项目“属性页”的“部署”选项卡中指定，并且也在解决方案资源管理器中可见。  
  
7.  在 SQL Server Management Studio 中，连接到 Analysis Services。 验证名为 **Analysis Services Tutorial** 的数据库是否正在服务器上运行。  
  
## <a name="next-step"></a>下一步  
您现在可以使用本教程了。 有关如何入门的详细信息，请参阅[多维建模（Adventure Works 教程）](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)。  
  
## <a name="see-also"></a>另请参阅  
[配置 Windows 防火墙以允许 Analysis Services 访问](../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[Configure the Windows Firewall to Allow SQL Server Access](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  