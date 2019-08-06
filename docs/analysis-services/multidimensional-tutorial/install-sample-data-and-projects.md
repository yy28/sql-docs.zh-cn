---
title: 安装 Analysis Services 示例数据和项目 |Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c89ee3edf9338c4f74b0738d930ee74dbec7244
ms.sourcegitcommit: bcc3b2c7474297aba17b7a63b17c103febdd0af9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794977"
---
# <a name="install-sample-data-and-multidimensional-projects"></a>安装示例数据和多维项目 
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

使用本文中提供的说明和链接来安装 Analysis Services 教程中使用的数据和项目文件。 
  
## <a name="step-1-install-prerequisites"></a>步骤 1：安装先决条件 
本教程中的课程假定您已安装以下软件。 您可以在一台计算机上安装所有功能。 若要安装这些功能，请运行 SQL Server 安装程序并从“功能选择”页中选择它们。  
  
-   SQL Server 数据库引擎  
  
-   SQL Server Analysis Services  (SSAS) 
  
    仅在以下版本中提供 Analysis Services:评估版、企业版、商业智能、标准版。 Azure Analysis Services 中不支持多维模型。
  
    默认情况下, Analysis Services 2016 和更高版本安装为表格实例, 你可以通过在安装向导的 "服务器配置" 页中选择 "多维服务器模式" 来覆盖此实例。
  
## <a name="step-2-download-and-install-developer-and-management-tools"></a>步骤 2：下载并安装开发人员和管理工具
Visual Studio 的 SQL Server Data Tools (SSDT) 与其他 SQL Server 功能分开下载和安装。 用于创建 BI 模型和报表的设计器和项目模板包含在 Visual Studio 2015 的 SSDT 中, 或作为 Visual Studio 2017 的[Nuget 包](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)。  
  
[下载 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=827542)。   

SQL Server Management Studio (SSMS) 与其他 SQL Server 功能分开下载和安装。  

[下载 SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)  

或者，请考虑安装 Excel 以便在您继续执行本教程时浏览您的多维数据。 通过安装 Excel，可以启用“在 Excel 中分析”功能。该功能可以使用连接到你要生成的多维数据集的数据透视表字段列表来启动 Excel。 建议使用 Excel 来浏览数据，因为您可以快速生成透视报表，并通过它与数据进行交互。  
  
或者，您可以使用在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中内置的内置 MDX 查询设计器来浏览数据。 查询设计器将返回相同的数据，除非数据以平面行集的形式表示。  
  
## <a name="step-3-install-databases"></a>步骤 3：安装数据库  
Analysis Services 多维模型使用您从关系数据库管理系统导入的事务数据。 出于本教程的目的, 请使用以下关系数据库作为数据源。  
  
-   **AdventureWorksDW2012 或更高版本**-这是在数据库引擎实例上运行的关系数据仓库。 它提供由您在本教程中生成和部署的 Analysis Services 数据库和项目使用的原始数据。 本教程假定你使用的是 AdventureWorksDW2012, 但是, 更高版本可以正常工作。
  
    您可以将此示例数据库与[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更高版本一起使用。 一般情况下, 应使用与数据库引擎版本匹配的示例数据库版本。
  
若要安装数据库, 请执行以下操作:  
  
1.  从 GitHub 下载[AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)数据库备份。  
  
2.  将备份文件复制到本地 SQL Server 数据库引擎实例的数据目录。
  
3.  启动 SQL Server Management Studio 并连接到数据库引擎实例。  
  
4.  还原数据库。  
  
## <a name="step-4-grant-database-permissions"></a>步骤 4：Grant 数据库权限  
示例项目使用数据源模拟设置，这些设置可指定导入或处理数据所用的安全上下文。 默认情况下，模拟设置指定用于访问数据的 Analysis Services 服务帐户。 若要使用此默认设置, 必须确保运行 Analysis Services 的服务帐户对**AdventureWorksDW**数据库具有数据读取器权限。  
  
> [!NOTE]  
> 出于学习的目的，建议您在 SQL Server 中使用默认服务帐户模拟选项并向服务帐户授予数据读取器权限。 尽管提供了其他模拟选项，但并非所有这些选项都适用于处理操作。 具体而言，使用当前用户的凭据的选项不支持处理操作。  
  
1.  确定服务帐户。 您可以使用 SQL Server 配置管理器或“服务”控制台应用程序来查看帐户信息。 如果使用默认帐户将 Analysis Services 作为默认实例安装，则该服务将作为 **NT Service\MSSQLServerOLAPService**运行。  
  
2.  在 Management Studio 中，连接到数据库引擎实例。  
  
3.  展开“安全性”文件夹，右键单击“登录名”，然后选择“新建登录名”。  
  
4.  在“常规”页的“登录名”中，键入 **NT Service\MSSQLServerOLAPService**（或运行该服务所用的任何帐户）。  
  
5.  单击“用户映射”。  
  
6.  选中**AdventureWorksDW**数据库旁边的复选框。 角色成员身份应自动包括 **db_datareader** 和 **public**。 单击“确定”接受默认值。  
  
## <a name="step-5-install-projects"></a>步骤 5：安装项目  

教程包括一些示例项目，以便您能将您的结果与完成的项目进行比较，或者学习后面的课程。  
  
1.  从 GitHub 上的 "Analysis Services 示例" 页中下载[adventure-works-multidimensional-tutorial-projects。](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services)  
  
    教程项目适用于[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更高版本。  
  
2.  将 .zip 文件移到根驱动器下一级的文件夹（例如 C:\Tutorial）。 如果你尝试在 "下载" 文件夹中解压缩这些文件, 则此步骤将会缓解有时会发生的 "路径过长" 错误。  
  
3.  解压缩示例项目：右键单击该文件，然后选择“全部提取”。 提取文件后, 应将文件夹第1、2、3、5、6、7、8、9、10完成和第4课的入门教程。 
  
4.  取消对这些文件的只读权限。 右键单击父文件夹, 选择 "**属性**", 并清除 "**只读**" 复选框。 单击 **“确定”** 。 将更改应用至此文件夹、子文件夹和文件。  

5.  打开与你所在的课程对应的解决方案 (.sln) 文件。 例如，在名为“Lesson 1 Complete”的文件夹中，您应打开 Analysis Services Tutorial.sln 文件。  
  
6.  部署解决方案以验证是否正确设置了数据库权限和服务器位置信息。  
  
    如果 Analysis Services 和数据库引擎是作为默认实例 (MSSQLServer) 安装的，并且所有软件在同一台计算机上运行，则可以单击“生成”菜单上的“部署解决方案”来生成示例项目并将其部署到本地 Analysis Services 实例。 在部署过程中, 将从本地数据库引擎实例上的**AdventureWorksDW**数据库处理 (或导入) 数据。 将在 Analysis Services 实例上创建一个新的 Analysis Services 数据库, 其中包含从数据库引擎检索的数据。  
  
    如果出现错误，请检查前面关于设置数据库权限的步骤。 此外，您还可能需要更改服务器名称。 默认服务器名称为 localhost。 如果服务器安装在远程计算机上或作为命名实例安装，必须覆盖默认名称以使用对于您的安装有效的服务器名称。 此外，如果服务器位于远程计算机上，则可能需要配置 Windows 防火墙以允许对它们进行访问。  
  
    用于连接到数据库引擎的服务器名称在多维解决方案的数据源对象中指定（《Adventure Works 教程》），并在解决方案资源管理器中可见。  
  
    用于连接到 Analysis Services 的服务器名称在项目“属性页”的“部署”选项卡中指定，并且也在解决方案资源管理器中可见。  
  
7.  在 SQL Server Management Studio 中，连接到 Analysis Services。 验证名为 **Analysis Services Tutorial** 的数据库是否正在服务器上运行。  
  
## <a name="next-step"></a>下一步  
您现在可以使用本教程了。 有关如何入门的详细信息，请参阅[多维建模（Adventure Works 教程）](multidimensional-modeling-adventure-works-tutorial.md)。  
  
## <a name="see-also"></a>请参阅  
[配置 Windows 防火墙以允许 Analysis Services 访问](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[Configure the Windows Firewall to Allow SQL Server Access](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  
