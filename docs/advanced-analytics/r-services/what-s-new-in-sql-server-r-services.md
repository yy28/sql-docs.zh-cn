---
title: "SQL Server R Services 中的新增功能 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 49986148fe9c7e929126e40debea1af8cff0bd13
ms.lasthandoff: 04/11/2017

---
# <a name="what39s-new-in-sql-server-r-services"></a>SQL Server R Services 中的新增功能
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 SQL Server vNext 中的功能，支持企业规模的数据科学。  R 是最受欢迎的用于高级分析的编程语言，提供而了异常丰富的程序包，并且具有一个充满活力并快速发展的开发人员社区。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 有助于在业务中采用高度普及的开放源代码 R 语言。 
  
 > [!TIP]
 > 已有 SQL Server 2016 R Services？
 > 现可在 2016 实例上安装最新版本的 Microsoft R Server，以便更频繁地更新 R 组件从而获益。 有关详细信息，请参阅 [Microsoft R Server 9.0.1](https://msdn.microsoft.com/microsoft-r/rserver-whats-new)。  

## <a name="whats-new-in-sql-server-vnext"></a>SQL Server vNext 中的新增功能
  
+ 引入 **MicrosoftML** 包

   来自 Microsoft R Server 和 Microsoft 数据科学团队的 MicrosoftML 是适用于 R 的新机器学习包。 只需通过几行代码，MicrosoftML 即可提高处理 R 模型中的大量文本数据和高维分类数据的速度、性能和规模。 此外，Microsoft R Server 客户可以访问 Azure 机器学习中包含的五个快速、精准的学习器。 
   
   有关详细信息，请参阅 [在 SQL Server R Services 中使用 MicrosoftML 包](../../advanced-analytics/r-services/using-the-microsoftml-package-with-sql-server-r-services.md)。
   
+ 针对数据科学家的更简单的包管理

  无需再依赖数据库管理员，就可以在 SQL Server 上安装所需的 R 包。 通过 **RevoScaleR** 中新的包安装和卸载函数，能从客户端计算机轻松安装和更新 R Services 中的包。 
  
  对于数据库管理员， [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 中包含的新角色可用于在实例级别和数据库级别管理与包关联的权限。 
  
  有关详细信息，请参阅 [SQL Server R Services 的 R 包管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。 
     
+ **RevoScaleR** 中的新函数用于读取和写入 R 模型对象

  现在，RevoScaleR 包含新的序列化函数以及更紧凑的模型存储格式，能快速加载和读取模型。 
  
  有关详细信息，请参阅 [使用 ODBC 保存和加载 SQL Server 中的 R 对象](../../advanced-analytics/r-services/save-and-load-r-objects-from-sql-server-using-odbc.md)。 

+ 通过**sqlrutils** 包，可更轻松地实现 SQL 集成

  此 R 包可帮助生成 R 代码的 SQL 存储过程调用。 然后可以在 SQL Server R Services 中使用生成的 SQL 存储过程。 提供的相关示例可帮助用户将 R 代码合并到可以在 SQL 存储过程中参数化的函数。
  
  有关详细信息，请参阅 [使用 sqlrutils 生成 R 代码的存储过程](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)。 
  

+ 便于 SSAS 连接的**olapR** 包

   此新包提供 R 和 SQL Server Analysis Services 连接的新维度，便于使用 OLAP 数据在 R 中进行分析。可以运行现有 MDX 查询并获取 R 数据框架，或通过在 R 代码中定义多维数据集轴和切片器来生成简单的 MDX 语句。 
   
   有关详细信息，请参阅 [在 R 中使用来自 OLAP 多维数据集的数据](../../advanced-analytics/r-services/using-data-from-olap-cubes-in-r.md)。
   

  
## <a name="features-in-sql-server-2016-r-services-and-sql-server-vnext"></a>SQL Server 2016 R Services 和 SQL Server vNext 中的功能  
  
- **RevoScaleR** 包用于通过 R 进行快速、可并行化的机器学习。

-   支持 SQL 登录和集成式 Windows 身份验证。  
    
-   显著的性能改进，包括优化 SQL 附属过程（这可连接 R 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]），支持数据分页以实现大批量数据使用，以及通过流式处理快速处理数十亿的行。 
  
-   使用 SQL Server 资源池管理 R 进程使用的内存。 有关详细信息，请参阅[创建外部资源池 (Transact-SQL)](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。  
  

### <a name="tools-and-setup"></a>工具和安装程序

-   轻松安装所有组件。 SQL Server 安装向导可以安装 **SQL Server R Services（数据库内）** 或 **Microsoft R Server（独立版）**。   运行安装向导时，如果要安装 SQL Server 实例，请选择 R Services；如果要安装数据科学工作站，请选择 R Server（独立版）。   有关安装选项的详细信息，请参阅[设置 SQL Server R Services（数据库内）](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)或[创建 R Server（独立版）](../../advanced-analytics/r-services/create-a-standalone-r-server.md)。  

-   如果不需要使用 SQL Server 中的数据，请考虑使用 [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)]。它可在多种平台上运行，并可为常用的开放源代码 R 语言提供企业级规模和性能。 [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)]。 有关详细信息，请参阅 MSDN 上的 [R Server（独立版）](../../advanced-analytics/r-services/r-server-standalone.md)或 [Introducing R Server](https://msdn.microsoft.com/microsoft-r/rserver)（R Server 简介）。

- 若要升级 SQL Server 2016 实例以使用 Microsoft R Server 9.0.1，请使用 [SqlBindR.exe 实用程序](https://msdn.microsoft.com/library/mt791781.aspx)。  

- [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-install) 是免费的 R 环境，包含生成在 R Services 或 R Server 上运行的 R 解决方案所需的所有工具和库。  

-   R Tools for Visual Studio 是一种适用于 Visual Studio 的免费插件，为 R 提供各种支持，包括标准 R 交互和变量窗口、R 函数的 Intellisense、调试和 R Markdown，并且能够导出到 Word 和 HTML。  有关详细信息，请参阅 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)。  

## <a name="learn-more"></a>了解详细信息
  
-  为想要了解 SQL Server 集成的数据科学家和希望使用 T-SQL 以及熟悉的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]环境创建 R 解决方案的 SQL 开发人员提供了资源。 
   + [SQL Server R Services 教程](https://msdn.microsoft.com/library/mt591993.aspx)
   + [免费电子书：SQL Server 2016 的数据科学](https://mva.microsoft.com/ebooks/)
 
+ 如果需要现成的解决方案，请使用 Microsoft 数据科学团队提供的 [机器学习模板](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/) ，这些模板演示了常见分析任务（包括预测维护和改动防护）的可行解决方案。
 

  
## <a name="see-also"></a>另请参阅  
[SQL Server vNext 中的新增功能](../../sql-server/what-s-new-in-sql-server-vnext.md)
  

