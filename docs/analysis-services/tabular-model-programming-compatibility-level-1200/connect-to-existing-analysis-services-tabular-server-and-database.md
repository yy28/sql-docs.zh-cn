---
title: 连接到现有的 Analysis Services 表格服务器和数据库 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13900e4aaad52d39a2691fb40d0e419f55f660fc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38033387"
---
# <a name="connect-to-existing-analysis-services-tabular-server-and-database"></a>连接到现有的 Analysis Services 表格服务器和数据库
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
SQL Server 2016 中 Analysis Services 管理对象 (AMO) 包括多个可用于设置服务器连接的命名空间。 本文介绍如何建立服务器连接的 Microsoft.AnalysisServices.Tabular 命名空间使用的模型和数据库创建在 1200年或更高的兼容性级别。 

若要连接到 Analysis Services 服务器，你的代码必须实例化服务器对象，然后对其调用 Connect 方法。 连接后，该服务器对象的属性将反映当前的 Analysis Services 实例的设置。 

对于顶级连接，可以使用以下类： 

* Microsoft.AnalysisServices.Server 
* Microsoft.AnalysisServices.Database 
* Microsoft.AnalysisServices.Tabular.Server 
* Microsoft.AnalysisServices.Tabular.Database 

正如您所看到的两个命名空间提供与服务器和数据库对象的连接： AMO 的原始 Microsoft.AnalysisServices 命名空间和 TOM 的新 Microsoft.AnalysisServices.Tabular 命名空间。

为什么进行相同的操作的两个命名空间？ 答案在于下游，在数据库和模型级别，其中对象层次结构成为特定于模式和模型树组成多维或表格元数据。 模型树中进行调用，这两种模型类型提供的服务器或数据库对象。

> [!NOTE]  
>  使用模型定义和操作的元数据是完全不同的两种模式。 通过将数据定义语言 (DDL) 分离到两个独立的命名空间，只需要为特定模型类型的 api 演示简化了开发体验。 

尽管 DDL 不同，但与服务器的连接是相同的跨所有模式、 版本和版本。 支持服务器和数据库连接是命名空间通过使您能够编写泛型工具或脚本连接到任何 Analysis Services 实例或数据库，而无需知道哪种类型的模型是在服务器上托管。  

这种灵活性介绍程序集之间的依赖关系。 为了调用 （例如，在表格 1200年数据库中，模型或多维数据集、 维度或度量值组多维或表格 1050年-1103年数据库内的） 上的数据库级别以下，AMO TOM 存在依赖关系。 

与此相反，TOM 不具有在 AMO 依赖关系。 尽管 TOM 不能用于浏览多维元数据 （多维数据集），但可以使用 AMO 来浏览多维和表格元数据。 

出于此原因，设置项目的第一步需要将引用添加到所有 AMO 程序集。 请参阅[安装，请参考和分发 TOM 客户端库](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md)有关详细信息。 

> [!NOTE]  
>  服务器和数据库连接基于旧版 AMO 类继承自 MajorObject。 尽管主要和次要对象不使用表格模型树中，但 MajorObject 类是用来设置连接而不考虑哪个 API 的服务器和数据库对象的基类的可见性。  

## <a name="code-example-server-connection"></a>代码示例： 服务器连接 

下面是演示如何连接到本地 Analysis Services 实例，并列出其属性在控制台窗口中的 C# 代码示例。 

此示例演示只有某些服务器对象的属性，但有更多属性，包括 ServerMode 和 DefaultCompatibilityLevel。  

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
运行此程序时，输出将显示在控制台窗口中的服务器对象上的属性。 

## <a name="authentication-and-authorization"></a>身份验证和授权 

服务器或数据库连接到 Analysis Services 需要管理权限，用于读写操作，以及通过模拟的连接请求。  

尽管已在最近几年，以允许在非常具体的情况下的自定义身份验证扩展 Analysis Services 安全基础结构，唯一受支持的外部身份验证方法是 Windows 集成的安全性。 安全主体假定是有效的 Windows 域用户或组帐户。  

在 Windows 2012 及更高版本，可以在域之间流动委派。 在 Analysis Services 中，委托仅用于 DirectQuery 模型中;否则，连接是直接或模拟。 

## <a name="next-steps"></a>后续步骤 

后建立连接，逻辑的下一步，将到任一列表中现有的数据库已在服务器上，或可能是创建新的空数据库。 以下链接包括代码示例演示了这两个基本任务： 

- [创建并部署空数据库](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)
- [列出现有的数据库](../../analysis-services/tabular-model-programming-compatibility-level-1200/list-existing-databases-on-a-tabular-server-analysis-services-amo-tom.md)
