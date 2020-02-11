---
title: 使用 Integration Services 加载
description: 提供使用 SQL Server Integration Services （SSIS）包将数据加载到并行数据仓库（PDW）的参考和部署信息。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b0bcb5cfe1ec4111aaea7153f35bca084df62b76
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401015"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>将 Integration Services 中的数据加载到并行数据仓库
提供使用 SQL Server Integration Services （SSIS）包将数据加载到 SQL Server 并行数据仓库的参考和部署信息。  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="Basics"></a>传授  
Integration Services 是对数据进行高性能提取、转换和加载（ETL）的 SQL Server 组件，通常用于填充和更新数据仓库。  
  
PDW 目标适配器是 Integration Services 组件，可让你使用 Integration Services .dtsx 包将数据加载到 PDW。 在 SQL ServerPDW 的包工作流中，可以从多个源加载和合并数据，并将数据加载到多个目标。 加载将在包内和同时运行的多个包中并行发生，直到在同一工具上并行运行最多 10 个加载。  
  
除了本主题中所述的任务之外，还可以使用 Integration Services 的其他功能在将数据加载到数据仓库中之前，对数据进行筛选、转换、分析和清理操作。 还可以通过运行 SQL 语句、运行子包或发送电子邮件，增强包的工作流。  
  
有关 Integration Services 的完整文档，请参阅[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)。  
  
## <a name="HowToDeployPackage"></a>用于运行 Integration Services 包的方法  
使用以下方法之一运行 Integration Services 包。  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>从 SQL Server 2008 R2 Business Intelligence Development Studio （投标）运行  
若要从投标内运行包，请右键单击包，然后选择 "**执行包**"。  
  
默认情况下，投标使用64位二进制文件运行包。 这是由**Run64BitRuntime** package 属性决定的。 若要设置此属性，请跳到**解决方案资源管理器**，右键单击项目，然后选择 "**属性**"。 在**Integration Services 属性页**上，中转到 "**配置属性**"，然后选择 "**调试**"。 你将在 "**调试" 选项**下看到 " **Run64BitRuntime** " 属性。 若要使用32位运行时，请将此项设置为**False**。 若要使用64位运行时，请将此值设置为**True**。  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>从 SQL Server 2012 SQL Server Data Tools 运行  
若要从 SQL Server Data Tools 中运行包，请右键单击包，然后选择 "**执行包**"。  
  
### <a name="run-from-powershell"></a>从 PowerShell 运行  
若要从 Windows PowerShell 使用**dtexec**实用工具运行包，请执行以下操作：`dtexec /FILE <packagePath>`  
  
例如： `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>从 Windows 命令提示符运行 
若要从 Windows 命令提示符运行包，请使用**dtexec**实用工具：`dtexec /FILE <packagePath>`  
  
例如： `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>数据类型  
使用 Integration Services 将数据从数据源加载到 SQL Server PDW 数据库时，会首先将数据从源数据映射到 Integration Services 数据类型。 这允许来自多个数据源的数据映射到一组通用的数据类型。  
  
然后，将数据从 Integration Services 映射到 SQL Server PDW 数据类型。 对于每个 SQL Server PDW 数据类型，下表列出了可转换为 SQL Server PDW 数据类型的 Integration Services 数据类型。  
  
|PDW 数据类型|映射到 PDW 数据类型的 Integration Services 数据类型|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|BIGINT|DT_I1、DT_I2、DT_I4、DT_I8、DT_UI1、DT_UI2、DT_UI4|  
|CHAR|DT_STR|  
|DATE|DT_DBDATE|  
|DATETIME|DT_DATE、DT_DBDATE、DT_DBTIMESTAMP、DT_DBTIMESTAMP2|  
|DATETIME2|DT_DATE、DT_DBDATE、DT_DBTIMESTAMP、DT_DBTIMESTAMP2|  
|DATETIMEOFFSET|DT_WSTR|  
|DECIMAL|DT_DECIMAL、DT_I1、DT_I2、DT_I4、DT_I4、DT_I8、DT_NUMERIC、DT_UI1、DT_UI2、DT_UI4、DT_UI8|  
|FLOAT|DT_R4、DT_R8|  
|INT|DT_I1、DTI2、DT_I4、DT_UI1、DT_UI2|  
|MONEY|DT_CY|  
|NCHAR|DT_WSTR|  
|NUMERIC|DT_DECIMAL、DT_I1、DT_I2、DT_I4、DT_I8、DT_NUMERIC、DT_UI1、DT_UI2、DT_UI4、DT_UI8|  
|NVARCHAR|DT_WSTR、DT_STR|  
|real|DT_R4|  
|SMALLDATETIME|DT_DBTIMESTAMP2|  
|SMALLINT|DT_I1、DT_I2、DT_UI1|  
|SMALLMONEY|DT_R4|  
|TIME|DT_WSTR|  
|TINYINT|DT_I1|  
|VARBINARY|DT_BYTES|  
|VARCHAR|DT_STR|  
  
**对数据类型精度的有限支持**  
  
PDW 如果映射的 DT_NUMERIC 或 DT_DECIMAL 输入列中包含的值的精度大于28，则会生成验证错误。  
  
**不支持的数据类型**  
  
SQL Server PDW 不支持以下 Integration Services 数据类型：  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
若要将包含这些类型数据的列加载到 SQL Server PDW 中，必须在数据流中添加一个上游数据转换，以将数据转换为兼容的数据类型。  
  
## <a name="permissions"></a>权限  
若要运行 Integration Services 加载包，需要：  
  
-   对数据库的 LOAD 权限。  
  
-   针对目标表的相应的 INSERT、UPDATE、DELETE 权限。  
  
-   如果使用临时数据库，则对临时数据库具有 CREATE 权限。 这适用于创建临时表。  
  
-   如果未使用任何临时数据库，则在目标数据库上创建权限。 这适用于创建临时表。  
  
## <a name="GenRemarks"></a>一般备注  
如果 Integration Services 包具有多个正在运行的 SQL Server PDW 目标，其中一个连接被终止，Integration Services 将停止向所有 SQL Server PDW 目标推送数据。  
  
## <a name="Limits"></a>限制和限制  
对于 Integration Services 包，相同数据源的 SQL Server PDW 目标数受最大活动负载的数目的限制。 该最大值是预先配置的，用户不可配置。 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
同一数据源的每个 Integration Services 包目标将计入包运行时的一个负载。 例如，假定处于活动状态的加载的最大数目为 10。 如果该包尝试为相同数据源打开 11 个或更多的目标，则该包将不运行。  
  
多个包可以同时运行，只要每个包所使用的处于活动状态的加载数目未超过该最大数目。 例如，如果处于活动状态的加载的最大数目为 10，则您可以同时运行两个包，每个包使用 10 个目标。 在一个包运行时，另一个包在加载队列中等待。  
  
如果加载队列中加载的数目超过排队的最大加载数，则该包将不运行。 例如，如果最大负载数为每个设备10个，并且每个设备的最大排队负载数为40，则可以并发运行每个打开的10个目标的五个 Integration Services 包。 如果您尝试运行第 6 个包，该包将不会运行。  

> [!IMPORTANT]
> 如果源表包含带有 SQL 排序规则的 char 和 varchar 列，则在 SSIS 中使用 OLE DB 数据源与 PDW 目标适配器，可能会导致数据损坏。 如果源表包含带有 SQL 排序规则的 char 或 varchar 列，我们建议使用 ADO.NET 源。 

  
## <a name="Locks"></a>锁定行为  
使用 Integration Services 加载数据时，SQL ServerPDW 使用行级锁来更新目标表中的数据。 这意味着，在更新每一行时，对于读取和写入操作，将锁定每一行。 在数据加载到临时表中时，将不锁定目标表中的行。  
  
## <a name="Examples"></a>示例  
  
### <a name="Walkthrough"></a>的. 平面文件的简单加载  
以下演练演示了使用 Integration Services 将平面文件数据加载到 SQL Server PDW 设备的简单数据加载。  此示例假设已在客户端计算机上安装了 Integration Services，并且已安装了 SQL Server PDW 目标，如上所述。  
  
在此示例中，我们将加载`Orders`到表中，该表具有以下 DDL。 `Orders`该表是`LoadExampleDB`数据库的一部分。  
  
```sql  
CREATE TABLE LoadExampleDB.dbo.Orders (  
   id INT,  
   city varchar(25),  
   lastUpdateDate DATE,  
   orderDate DATE)  
;  
```  
  
下面是加载数据：  
  
```  
id        city           lastUpdateDate     orderdate  
--------- -------------- ------------------ ----------  
1         Seattle        2010-05-01         2010-01-01  
2         Denver         2002-06-25         1999-01-02  
```  
  
为实现负载准备，请创建包含负载数据`exampleLoad.txt`的平面文件：  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
首先，通过执行以下步骤创建 Integration Services 包：  
  
1.  在 SQL Server Data Tools \(SSDT\)中，依次选择 "**文件**"、"**新建**" 和 "**项目**"。 从列出的选项中选择 " **Integration Services 项目**"。 为此项目`ExampleLoad`命名，然后单击 **"确定"**。  
  
2.  单击 "**控制流**" 选项卡，然后将 "数据流**任务**" 从 "**工具箱**" 拖动到 "**控制流**" 窗格。  
  
3.  单击 "**数据流" 选项卡**，然后将 "**平面文件源**" 从**工具箱**拖到 **"数据流" 窗格。** 双击刚创建的框以打开 "**平面文件源编辑器**"。  
  
4.  单击 "**连接管理器**"，然后单击 "**新建**"。  
  
5.  在 "**连接管理器名称**" 框中，为连接输入一个友好名称。 对于本示例， `Example Load Flat File CM`为。  
  
6.  单击 "**浏览**" 并`ExampleLoad.txt`从本地计算机中选择文件。  
  
7.  由于平面文件包含具有列名称的行，因此请**在第一个数据行框中单击列名称**。  
  
8.  单击左栏中的 "**列**"，并预览将加载的数据，以确保正确解释列名和数据。  
  
9. 在左列中单击 "**高级**"。 单击每个列名，查看与数据关联的数据类型。 在框中键入更改，以使所加载数据的数据类型与目标列类型兼容。  
  
10. 单击 **"确定"** 以保存连接管理器。  
  
11. 单击 **"确定"** 退出 "**平面文件源编辑器**"。  
  
指定数据流的目标。  
  
1.  将**SQL Server PDW 目标**从 "**工具箱**" 拖动到 **"数据流" 窗格。**  
  
2.  双击刚创建的框以加载 " **SQL Server PDW 目标编辑器**"。  
  
3.  单击 "**连接管理器**" 旁的向下箭头。  
  
4.  选择 "**创建新连接**"。  
  
5.  为服务器、用户、密码和目标数据库填写信息，其中包含特定于设备的信息。 （示例如下所示）。 然后单击“确定”  。  
  
    对于 "未实现连接"，**服务器名称**：输入 <设备名称>-SQLCTL01、17001。  
  
    对于 "以太网连接"，**服务器名称**：输入控制节点群集的 IP 地址，逗号，端口17001。 例如，10.192.63.134、17001。  
  
    **用户**`user1`  
  
    **权限**`password1`  
  
    **目标数据库：**`LoadExampleDB`  
  
6.  选择目标表： `Orders`。  
  
7.  选择 "**追加**" 作为加载模式，然后单击 **"确定"**。  
  
指定从源到目标的数据流。  
  
1.  在 "**数据流" 窗格上**，将绿色箭头从 "**平面文件源**" 框拖到 " **SQL Server PDW 目标**" 框。  
  
2.  双击 " **SQL Server PDW 目标**" 框，以便再次看到 " **SQL Server PDW 目标编辑器**"。 你应在 "未**映射的输入列**" 下的左侧平面文件中看到列名。 应会在右侧的 "未**映射的目标列**" 下看到目标表中的列名称。 拖动或双击 "未**映射的输入列**"**和 "未**映射的**目标列**" 列表中的匹配列名称，以映射列。 单击 **"确定"** 以保存设置。  
  
3.  通过单击 "**文件**" 菜单中的 "**保存**" 来保存包。  
  
在计算机上运行包 Integration Services。  
  
1.  在 Integration Services**解决方案资源管理器**（右列）中，右键单击`Package.dtsx`并选择 "**执行**"。  
  
2.  将运行包，**进度窗格上将显示进度以及**任何错误。 使用 SQL 客户端确认负载，或通过 SQL Server PDW 管理控制台监视负载。  
  
## <a name="see-also"></a>另请参阅  
[创建使用 SSIS PDW 目标适配器的脚本任务](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
[设计和实现包 (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[教程：使用向导创建基本包](https://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[入门（Integration Services）](https://go.microsoft.com/fwlink/?LinkId=202412)  
[动态包生成示例](https://go.microsoft.com/fwlink/?LinkId=202413)  
[设计 SSIS 包以实现并发性（SQL Server 视频）](https://msdn.microsoft.com/library/dd795221.aspx)  
[Microsoft SQL Server 社区示例： Integration Services](https://go.microsoft.com/fwlink/?LinkId=202415)  
[通过变更数据捕获改善增量加载](../integration-services/change-data-capture/change-data-capture-ssis.md)  
[渐变维度转换](../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
[大容量插入任务](../integration-services/control-flow/bulk-insert-task.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
