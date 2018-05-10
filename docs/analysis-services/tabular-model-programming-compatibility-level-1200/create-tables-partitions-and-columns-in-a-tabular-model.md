---
title: 在表格模型中创建表、 分区和列 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8908697bc274c756de8ca74d8a1036417aa5f9b2
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="create-tables-partitions-and-columns-in-a-tabular-model"></a>在表格模型中创建表、 分区和列
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
在表格模型中，表由行和列组成。 行组织成分区，以支持增量数据刷新。 表格解决方案可以支持几种类型的表，具体取决于数据来源于何处：  

* 普通表，数据从关系数据源，通过数据提供程序的来源位置。 

* 按下的表，其中数据被"推送"到表以编程方式。 

* 计算的表，其中数据来自引用另一个对象的数据模型中的 DAX 表达式。  

在下面的代码示例中，我们将定义常规表。 

## <a name="required-elements"></a>必需的元素 

表必须具有至少一个分区。 常规表还必须定义至少一个列。 

每个分区必须具有指定的数据源的源，但可以设置源为 null。 通常情况下，源是相关数据库查询语言中定义的数据切片的查询表达式。 

## <a name="code-example-create-a-table-column-parition"></a>代码示例： 创建表、 列、 分区

表由表类中 （位于 Microsoft.AnalysisServices.Tabular 命名空间） 表示。 

在下面的示例中，我们将定义常规表具有一个链接到关系数据源和少量的正则列的分区。 我们还将提交到服务器的更改并触发数据刷新将纳入模型的数据。 当你想要将数据从 SQL Server 关系数据库加载到表格解决方案时，这表示最典型的情形。 


```
using System; 
using Microsoft.AnalysisServices; 
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
                // Generate a new database name and use GetNewName 
                // to ensure the database name is unique. 
                // 
                string newDatabaseName = 
                    server.Databases.GetNewName("Database with a Table Definition"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var dbWithTable = new Database() 
                { 
                    Name = newDatabaseName, 
                    ID = newDatabaseName, 
                    CompatibilityLevel = 1200, 
                    StorageEngineUsed = StorageEngineUsed.TabularMetadata, 
                }; 
 
                // 
                // Add a Microsoft.AnalysisServices.Tabular.Model object to the 
                // database, which acts as a root for all other Tabular metadata objects. 
                // 
                dbWithTable.Model = new Model() 
                { 
                    Name = "Tabular Data Model", 
                    Description = "A Tabular data model at the 1200 compatibility level." 
                }; 
 
                // 
                // Add a Microsoft.AnalysisServices.Tabular.ProviderDataSource object 
                // to the data Model object created in the previous step. The connection 
                // string of the data source object in this example  
                // points to an instance of the AdventureWorks2014 SQL Server database. 
                // 
                string dataSourceName = "SQL Server Data Source Example"; 
                dbWithTable.Model.DataSources.Add(new ProviderDataSource() 
                { 
                    Name = dataSourceName, 
                    Description = "A data source definition that uses explicit Windows credentials for authentication against SQL Server.", 
                    ConnectionString = "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureWorks2014;Integrated Security=SSPI;Persist Security Info=false", 
                    ImpersonationMode = Microsoft.AnalysisServices.Tabular.ImpersonationMode.ImpersonateAccount, 
                    Account = @".\Administrator", 
                    Password = "P@ssw0rd", 
                }); 
 
                //  
                // Add a table called Individual Customers to the data model 
                // with a partition that points to a [Sales].[vIndividualCustomer] view 
                // in the underlying data source. 
                // 
                dbWithTable.Model.Tables.Add(new Table() 
                { 
                    Name = dbWithTable.Model.Tables.GetNewName("Individual Customers"), 
                    Description = "Individual customers (names and email addresses) that purchase Adventure Works Cycles products online.", 
                    Partitions = { 
                        // 
                        // Create a single partition with a QueryPartitionSource for a query 
                        // that imports all customer rows from the underlying data source. 
                        // 
                        new Partition() { 
                            Name = "All Customers", 
                            Source = new QueryPartitionSource() { 
                                DataSource = dbWithTable.Model.DataSources[dataSourceName], 
                                Query = @"SELECT   [FirstName] 
                                                    ,[MiddleName] 
                                                    ,[LastName] 
                                                    ,[PhoneNumber]  
                                                    ,[EmailAddress] 
                                                    ,[City] 
                                        FROM [Sales].[vIndividualCustomer]", 
                            } 
                        } 
                    }, 
                    Columns = 
                    { 
                        // 
                       // DataColumn objects refer to regular table columns.  
                        // Each DataColumn object corresponds to a column in the underlying data source query. 
                        // 
                        new DataColumn() { 
                            Name = "FirstName", 
                            DataType = DataType.String, 
                            SourceColumn = "FirstName", 
                        }, 
                        new DataColumn() { 
                            Name = "MiddleName", 
                            DataType = DataType.String, 
                            SourceColumn = "MiddleName", 
                        }, 
                        new DataColumn() { 
                            Name = "LastName", 
                            DataType = DataType.String, 
                            SourceColumn = "LastName", 
                        }, 
                        new DataColumn() { 
                            Name = "PhoneNumber", 
                            DataType = DataType.String, 
                            SourceColumn = "PhoneNumber", 
                        }, 
                        new DataColumn() { 
                            Name = "EmailAddress", 
                            DataType = DataType.String, 
                            SourceColumn = "EmailAddress", 
                        }, 
                        new DataColumn() { 
                            Name = "City", 
                            DataType = DataType.String, 
                            SourceColumn = "City", 
                        }, 
                    } 
                }); 
 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(dbWithTable); 
 
                //  
                // Request a full refresh to import the data from the data source and 
                // and perform any necessary recalculations. 
                // The refresh operation will be performed with the next 
                // invocation of Model.SaveChanges() or Database.Update(UpdateOptions.ExpandFull). 
                dbWithTable.Model.RequestRefresh(Microsoft.AnalysisServices.Tabular.RefreshType.Full); 
                dbWithTable.Update(UpdateOptions.ExpandFull); 
 
 
                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(dbWithTable.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
 
                Console.WriteLine("The data model includes the following table definitions:"); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                foreach (Table tbl in dbWithTable.Model.Tables) 
                { 
                    Console.WriteLine("\tTable name:\t\t{0}", tbl.Name); 
                    Console.WriteLine("\ttbl description:\t{0}", tbl.Description); 
                } 
                Console.ResetColor(); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```

## <a name="partitions-in-a-table"></a>表中的分区 

分区表示通过**分区**（位于 Microsoft.AnalysisServices.Tabular 命名空间） 的类。 **分区**类会公开**源**P 属性**artitionSource**键入，其中一种抽象基础上提供了不同的方法引入到的数据分区。 A**分区**实例可以具有**源**，该值指示，数据将会被推送到分区通过将数据块作为的一部分发送到服务器的属性为 null，推送数据 API 公开的 Analysis Services. SQL Server 2016 中**PartitionSource**类具有两个派生的类表示方式将数据绑定到一个分区： **QueryPartitionSource**和**CalculatedPartitionSource**. 

## <a name="columns-in-a-table"></a>表中的列 

列表示由几个类派生自基**列**（位于 Microsoft.AnalysisServices.Tabular 命名空间） 的类： 

* **DataColumn** （对于普通表的正则列）
* **CalculatedColumn** （对于支持的 DAX 表达式的列）
* **CalculatedTableColumn** （对于计算表中的正则列）
* **RowNumberColumn** （为每个表创建的 SSAS 的列的特殊类型）。 

## <a name="row-numbers-in-a-table"></a>在表中的行号 

每个**表**在服务器上的对象具有**RowNumberColumn**在进行索引时使用。 无法创建或将其显式添加。 保存或更新对象时，将自动创建列： 

* **db。SaveChanges** 

* **db。Update(ExpandFull)** 

调用任一方法时，服务器将行号列自动创建，这将会显示为**RowNumberColumn**表的列集合。 

## <a name="calculated-tables"></a>计算表 

计算的表源自重新规划数据从模型中的现有数据结构或外部的绑定的 DAX 表达式。 若要以编程方式创建计算的表，请执行以下操作： 

* 创建常规**表**。 

* 使用类型的源将分区添加到它**CalculatedPartitionSource**，其中源是 DAX 表达式。 分区的源是什么将常规表和计算表区分开来。 

当所做的更改保存到服务器时，则服务器将返回的推断的列表**CalculatedTableColumns** （计算表组成计算的表中的列），通过表的列集合可见。 

## <a name="next-steps"></a>后续步骤

查看用于在 TOM 中处理异常的类：[在 TOM 中处理错误](../../analysis-services/tabular-model-programming-compatibility-level-1200/handling-errors-in-the-tom-api-analysis-services-amo-tom.md)
  
