---
title: "连接到现有的 Analysis Services 表格服务器和数据库 |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 05be704e-4ee4-4101-b5ce-96fdda18c639
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 061b37f5b0e8209f896ded915f0259c3253a1439
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="connect-to-existing-analysis-services-tabular-server-and-database"></a>连接到现有的 Analysis Services 表格服务器和数据库

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

在 SQL Server 2016 Analysis Services 管理对象 (AMO) 包括多个无法用于建立服务器连接的命名空间。 此文章介绍了如何建立服务器连接的模型和在 1200年创建的数据库使用的 Microsoft.AnalysisServices.Tabular 命名空间或更高版本的兼容性级别。 

若要连接到 Analysis Services 服务器，你的代码必须实例化服务器对象，然后对其调用连接方法。 连接后，该服务器对象的属性将反映当前的 Analysis Services 实例的设置。 

下面的类可以用于顶级连接： 

* Microsoft.AnalysisServices.Server 
* Microsoft.AnalysisServices.Database 
* Microsoft.AnalysisServices.Tabular.Server 
* Microsoft.AnalysisServices.Tabular.Database 

如你所见，两个命名空间提供与服务器和数据库对象的连接： AMO 的原始 Microsoft.AnalysisServices 命名空间和 TOM 的新 Microsoft.AnalysisServices.Tabular 命名空间。

为什么为相同的操作的两个命名空间？ 答案介于下游，在数据库和模型级别，其中对象层次结构将为特定模式的并且将模型树组成多维或表格元数据。 若要在模型树中进行调用，这两个模型类型提供的服务器或数据库对象。

> [!NOTE]  
>  用于模型定义和操作的元数据是完全不同的两种模式。 通过将数据定义语言 (DDL) 分离到两个单独的命名空间，简化了开发体验，通过所需的特定模型类型 API 演示文稿。 

尽管 DDL 不同，与服务器的连接将是相同的所有模式、 版本和版本。 支持的服务器和数据库连接通过任一命名空间允许你编写泛型工具或连接到任何 Analysis Services 实例的脚本或数据库，而无需了解哪种类型的模型是服务器上托管。  

这种灵活性说明的程序集中的依赖关系。 为了在数据库级别 （例如，对在表格 1200年数据库中，模型或多维数据集、 维度或多维或表格 1050年 1103年数据库内的度量值组） 之下进行调用，AMO TOM 上具有依赖关系。 

与此相反，TOM 不具有在 AMO 依赖项。 尽管 TOM 不能用于浏览多维元数据 （多维数据集），但可以使用 AMO 来浏览多维和表格元数据。 

为此，设置你的项目的第一步，需要添加对所有 AMO 程序集的引用。 请参阅[安装引用和分发 TOM 客户端库](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md)有关详细信息。 

> [!NOTE]  
>  服务器和数据库连接基于从 MajorObject 继承的旧版 AMO 类。 尽管在表格模型树中不使用主版本号和次对象，MajorObject 类是用来设置连接而不考虑哪些 API 的服务器和数据库对象的基类的可见性。  

## <a name="code-example-server-connection"></a>代码示例： 服务器连接 

下面是演示如何连接到本地的 Analysis Services 实例，并列出其属性在控制台窗口中的 C# 代码示例。 

此示例演示只有某些服务器对象，对象的属性，但有可用的更多属性，包括 ServerMode 和 DefaultCompatibilityLevel。  

```
using System; 
using Microsoft.AnalysisServices.Tabular; 

namespace TOMSamples 
{ 
    class Program 
    { 
        static void Main(string[] args) 
        { 
            // 
            // Connect to the local default instance of Analysis Services 
            // 
            string ConnectionString = "DataSource=localhost"; 


            // 
            // The using syntax ensures the correct use of the 
            // Microsoft.AnalysisServices.Tabular.Server object. 
            // 
            using (Server server = new Server()) 
            { 
                server.Connect(ConnectionString); 

 
                Console.WriteLine("Connection established successfully."); 
                Console.WriteLine(); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.WriteLine("Server name:\t\t{0}", server.Name); 
                Console.WriteLine("Server product name:\t{0}", server.ProductName); 
                Console.WriteLine("Server product level:\t{0}", server.ProductLevel); 
                Console.WriteLine("Server version:\t\t{0}", server.Version); 
                Console.ResetColor(); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```
运行此程序时，该输出将显示在控制台窗口中的服务器对象上的属性。 

## <a name="authentication-and-authorization"></a>身份验证和授权 

服务器或数据库连接到 Analysis Services 需要管理权限，使用对于读写操作，以及通过模拟的连接请求将传递。  

尽管 Analysis Services 安全基础结构已扩展在最近几年，以允许在非常特定条件下的自定义身份验证，唯一支持的外部身份验证方法是 Windows 集成的安全性。 安全主体被假定为有效的 Windows 域用户或组帐户。  

Windows 2012 及更高版本，则可以在域之间流动委派。 在 Analysis Services 中，委派仅用于 DirectQuery 模型;否则，连接是直接或模拟。 

## <a name="next-steps"></a>后续步骤 

在建立连接后, 逻辑的下一步是已在服务器上，或者列出现有数据库，或可能会创建新的空数据库。 以下链接包括代码示例演示这两项基本任务： 

- [创建和部署一个空数据库](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)
- [列出现有的数据库](../../analysis-services/tabular-model-programming-compatibility-level-1200/list-existing-databases-on-a-tabular-server-analysis-services-amo-tom.md)

