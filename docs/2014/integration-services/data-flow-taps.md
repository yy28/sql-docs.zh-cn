---
title: 数据流点击 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2d847adf-4b3d-4949-a195-ef43de275077
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 053b34add45354d0df71fa73a72f8786cc706d15
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432434"
---
# <a name="data-flow-taps"></a>数据分流
  [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 引入了一个新功能，可用来在运行时在包数据流路径上添加数据分流点，并将数据分流点的输出定向到外部文件。 若要使用此功能，您必须使用项目部署工具将 SSIS 项目部署到 SSIS 服务器。 将包部署到服务器之后，需要对 SSISDB 数据库执行 T-SQL 脚本，以便在执行该包之前添加数据分流点。 下面是一个示例方案：  
  
1.  通过使用 [catalog.create_execution（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database)存储过程，创建包的执行实例。  
  
2.  通过使用 [catalog.add_data_tap](/sql/integration-services/system-stored-procedures/catalog-add-data-tap) 或 [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid) 存储过程，添加数据分流点。  
  
3.  使用 [catalog.start_execution（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)，启动包的执行实例。  
  
 下面是执行上述方案中所述步骤的示例 SQL 脚本：  
  
```  
  
Declare @execid bigint  
EXEC [SSISDB].[catalog].[create_execution] @folder_name=N'ETL Folder', @project_name=N'ETL Project', @package_name=N'Package.dtsx', @execution_id=@execid OUTPUT  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt'  
EXEC [SSISDB].[catalog].[start_execution] @execid  
  
```  
  
 该 create_execution 存储过程的文件夹名称、项目名称和包名称参数对应于 Integration Services 目录中的文件夹、项目和包名称。 如下图所示，您可以从 SQL Server Management Studio 获取在 create_execution 调用中使用的文件夹、项目和包名称。 如果您在这里没有看到该 SSIS 项目，则可能还未将该项目部署到 SSIS 服务器。 在 Visual Studio 中右键单击 SSIS 项目，然后单击“部署”以将该项目部署到目标 SSIS 服务器。  
  
 您可以不键入 SQL 语句，而是通过执行以下步骤来生成执行包脚本：  
  
1.  右键单击“Package.dtsx”****，然后单击“执行”****。  
  
2.  单击 **“脚本”** 工具栏按钮以生成脚本。  
  
3.  现在，在 start_execution 调用的前面添加 add_data_tap 语句。  
  
 add_data_tap 存储过程的 task_package_path 参数对应于 Visual Studio 中数据流任务的 PackagePath 属性。 在 Visual Studio 中，右键单击“数据流任务”****，然后单击“属性”**** 启动“属性”窗口。  请记下 **PackagePath** 属性的值，以将其用作 add_data_tap 存储过程调用的 task_package_path 参数值。  
  
 add_data_tap 存储过程的 dataflow_path_id_string 参数对应于您要添加数据分流点的数据流路径的 IdentificationString 属性。 若要获取 dataflow_path_id_string，请单击数据流路径（数据流中任务间的箭头），并记下“属性”窗口中 **IdentificationString** 属性的值。  
  
 执行脚本时，输出文件存储在 \<Program Files> \MICROSOFT SQL server\110\dts\datadumps 中。中。 如果已存在同名文件，则将创建带有后缀的新文件（例如：output[1].txt）。  
  
 如前所述，也可使用 [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid)存储过程代替使用 add_data_tap 存储过程。 此存储过程将数据流任务的 ID 用作参数，而不使用 task_package_path。 您可以从 Visual Studio 中的属性窗口获取数据流任务的 ID。  
  
## <a name="removing-a-data-tap"></a>删除数据分流点  
 可使用 [catalog.remove_data_tap](/sql/integration-services/system-stored-procedures/catalog-remove-data-tap) 存储过程删除数据分流点，然后再启动执行。 此存储过程将数据分流点 ID 用作参数，此 ID 可作为 add_data_tap 存储过程的输出来获取。  
  
```  
  
DECLARE @tap_id bigint  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt' @data_tap_id=@tap_id OUTPUT  
EXEC [SSISDB].[catalog].remove_data_tap @tap_id  
  
```  
  
## <a name="listing-all-data-taps"></a>列出所有数据分流点  
 您也可以使用 catalog.execution_data_taps 视图列出所有数据分流点。 下面的示例提取一个规范执行实例（ID：54）的数据分流点。  
  
```  
select * from [SSISDB].[catalog].execution_data_taps where execution_id=@execid  
```  
  
## <a name="performance-consideration"></a>性能注意事项  
 启用详细日志记录级别并添加数据分流点会增加数据集成解决方案所执行的 I/O 操作数。 因此，建议仅出于故障排除目的添加数据分流点。  
  
## <a name="video"></a>视频  
 此 [video on TechNet](https://technet.microsoft.com/sqlserver/dn600163) 演示了如何在 SQL Server 2012 SSISDB 目录中添加/使用数据分流点，从而有助于以编程方式对包进行调试并在运行时捕获部分结果。 它还讨论了如何列出/删除这些数据分流点，并讨论了在 SSIS 包中使用数据分流点的最佳实践。  
  
## <a name="related-tasks"></a>Related Tasks  
 [调试数据流](troubleshooting/debugging-data-flow.md)  
  
 [对包执行进行故障排除的工具](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
