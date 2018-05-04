---
title: 列出在表格服务器 (Analysis Services AMO-TOM) 上的现有数据库 |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ab5eb4b8-6254-442d-a42e-2372c346d260
caps.latest.revision: 2
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5386b96d66de38d29909eb4fbf5fb3498c01daec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="list-existing-databases-on-a-tabular-server-analysis-services-amo-tom"></a>列出在表格服务器 (Analysis Services AMO-TOM) 上的现有数据库
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
如果你具有**服务器**对象，该对象连接到 Analysis Services 实例，可以循环访问**Server.Databases**列出 Anlaysis Services 实例所承载的所有数据库的集合。 

**Server.Databases**集合包含一个**数据库**托管在服务器上，而不考虑服务器模式 （Multidimensional 或 Tabular） 或数据库类型 （多维，每个数据库对象以前的 1200 表格或表格 1200年和更高版本）。 

你可以检查的一种通过数据库**Database.StorageEngineUsed**属性。  

表格 1200年和更高版本数据库将返回非 null **Database.Model**访问的表格元数据的所有对象的属性： 表、 列、 关系和等等。  

对于多维或 1103 表格并将下面 Database.Model 属性将为 null。 在这种情况下，非表格元数据将可在多维属性 （如 Database.Cubes 和 Database.Dimensions），但这些属性仅公开由 Microsoft.AnalysisServices.Database 类 （从 AMO)，而不是由（对于 TOM) Microsoft.AnalysisServices.Tabular.Database。 有关要使用哪个数据库类的详细信息，请参阅[安装，请将分发，并引用 TOM 客户端库](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md)。

除非 Database.StorageEngineUsed 设置为 TabularMetadata，你将无法使用表格命名空间中的其他类来访问或对模型树进行操作。 

连接到服务器或数据库服务器或数据库上使用 Microsoft.AnalysisServices.Tabular 类时下, 表总结了预期的行为。 

mode | Database.model | Database.StorageEngineUsed
-----|----------------|---------------------------
表格 1200年 1400年 | 返回模型的名称| StorageEngineUsed.TabularMetadata 
1103 表格 1100年、 1050年 | 返回 null | StorageEngineUsed.InMemory 
多维 | 返回 null | StorageEngineUsed.Traditional 

## <a name="code-example-list-existing-databases"></a>代码示例： 列出现有的数据库

下面的代码演示如何连接到服务器所承载的服务器和列表数据库。 

```
using System; using Microsoft.AnalysisServices; 
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

                 // 
                // List common properties for the databases on the server. 
                // 
                foreach (Database db in server.Databases) 
                { 
                    Console.WriteLine("Properties for database {0}:", db.Name); 
                    Console.ForegroundColor = ConsoleColor.Yellow; 
                    Console.WriteLine("Database ID:\t\t\t{0}", db.ID); 
                    Console.WriteLine("Database compatibility level:\t{0}", db.CompatibilityLevel); 
                    Console.WriteLine("Database collation:\t\t{0}", db.Collation); 
                    Console.WriteLine("Database created timestamp:\t{0}", db.CreatedTimestamp); 
                    Console.WriteLine("Database language ID:\t\t{0}", db.Language); 
                    Console.WriteLine("Database model type:\t\t{0}", db.ModelType); 
                    Console.WriteLine("Database state:\t\t\t{0}", db.State); 
                    Console.ResetColor(); 
                    Console.WriteLine(); 
                } 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```


## <a name="get-an-item-from-a-database"></a>从数据库中获取项 

下面的代码段演示如何获取表格或数据库中的列。 


```
var db = srv.Databases.GetByName("abc"); 

Column c1 = db.Model.Tables["foo"].Columns["bar"]; 
if (c1.ObjectType == ObjectType.Column) // always true 

MetadataObject obj; 

switch(obj.ObjectType) 
{ 
 case ObjectType.Table: 
  var t1 = (Table)obj; 
  break; 
} 
```

## <a name="next-steps"></a>后续步骤

了解如何[创建和部署一个空数据库](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)使用 TOM API。

