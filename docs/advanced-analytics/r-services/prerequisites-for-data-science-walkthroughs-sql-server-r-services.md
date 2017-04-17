---
title: "数据科学演练的先决条件 (SQL Server R Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/22/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 04485527230988a0ef8b6eddfe76d49007bef5dd
ms.lasthandoff: 04/11/2017

---
# <a name="prerequisites-for-data-science-walkthroughs-sql-server-r-services"></a>数据科学演练的先决条件 (SQL Server R Services)
我们建议在可以连接到同一网络上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机的 R 工作站上运行演练。 还可在同时具有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 R 开发环境的计算机上运行演练。 
  
  
## <a name="install-sql-server-2016-r-services-in-database"></a>安装 SQL Server 2016 R Services (In-Database)  
必须具有对安装了 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 实例的访问权限。 有关如何设置 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]的详细信息，请参阅 [设置 SQL Server R Services (In-Database)](https://msdn.microsoft.com/library/mt696069.aspx)。  
  
  
> [!IMPORTANT]  
> 请务必使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或更高版本。 以前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持与 R 集成。但是，可使用旧版的 SQL 数据库作为 ODBC 数据源。  
  
## <a name="install-an-r-development-environment"></a>安装 R 开发环境  
若要在计算机上完成本演练，将需要 R 开发环境，或任何其他可以运行 R 命令的命令行工具。    
  
- **R Tools for Visual Studio** 是一款免费插件，可为 Microsoft R Server 和 SQL Server R Services 提供 Intellisense、调试和支持。 若要下载，请参阅 [R Tools for Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx)。  
    
- **Microsoft R Client** 是一种轻型开发工具，支持使用 ScaleR 包在 R 中进行开发。 若要了解此工具，请参阅 [Microsoft R 客户端入门](https://msdn.microsoft.com/microsoft-r/r-client-get-started)。
  
- **RStudio** 是广受欢迎的 R 开发环境之一。 有关详细信息，请参阅 [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)。  
  
    但是，不能使用 RStudio 的通用安装或其他环境完成本教程；还必须为 Microsoft R Open 安装 R 包和连接库。 有关详细信息，请参阅 [设置数据科学客户端](https://msdn.microsoft.com/library/mt696067.aspx)。  

- 安装 [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]时，将默认安装 R 工具（R.exe、RTerm.exe、RScripts.exe）。 如果不想安装 IDE，可以使用这些工具。  
  
  
## <a name="get-permissions-to-connect-to-sql-server"></a>获取连接到 SQL Server 的权限  
在本演练中，将连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，以运行脚本和上传数据。 为此，必须具有有效的数据库服务器登录凭据。  可以使用 SQL 登录凭据或集成 Windows 身份验证信息。 让数据库管理员为你在服务器上创建一个帐户，使其具有对在其中使用 R 的数据库的以下权限：  
  
-   创建数据库、表、函数和存储过程    
-   将数据插入到表中  
  
  
## <a name="start-the-walkthrough"></a>开始演练  
[第 1 课：准备数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  


