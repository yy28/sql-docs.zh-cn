---
title: 加载带有 Integration Services 的并行数据仓库 |Microsoft 文档
description: 提供有关使用 SQL Server Integration Services (SSIS) 包来加载数据到并行数据仓库 (PDW) 的引用和部署信息。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 718a076822a4304e0ba951f3ca1903bb7c009e17
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34586059"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>使用 Integration Services 并行数据仓库加载数据
提供数据加载到 SQL Server 并行数据仓库，通过使用 SQL Server Integration Services (SSIS) 包的引用和部署的信息。  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](http://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="Basics"></a>基础知识  
集成服务是高性能提取、 转换和加载 (ETL) 的数据，SQL Server 组件，通常用于填充和更新数据仓库。  
  
PDW 目标适配器是允许你通过使用 Integration Services dtsx 包数据加载到 PDW 的 Integration Services 组件。 在 SQL ServerPDW 包流中，你可以加载和合并来自多个源的数据和数据加载到多个目标。 加载将在包内和同时运行的多个包中并行发生，直到在同一工具上并行运行最多 10 个加载。  
  
除了本主题中所述的任务，可以使用 Integration Services 的其他功能来筛选、 转换、 分析，并在加载到数据仓库之前清理数据。 还可以通过运行 SQL 语句、运行子包或发送电子邮件，增强包的工作流。  
  
Integration Services 的完整文档，请参阅[SQL Server Integration Services](http://msdn.microsoft.com/library/ms141026(v=sql11).aspx)。  
  
## <a name="HowToDeployPackage"></a>运行 Integration Services 包方法  
使用下列方法之一运行 Integration Services 包。  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>从 SQL Server 2008 R2 Business Intelligence Development Studio (BIDS) 中运行  
若要运行从 BIDS 内的包，右键单击你的包，然后选择**执行包**。  
  
默认情况下，BIDS 运行使用 64 位二进制文件的包。 这由**Run64BitRuntime**包属性。 若要设置此属性，请转到**解决方案资源管理器**，右键单击你的项目，然后选择**属性**。 上**集成服务属性页**，请转到**配置属性**和选择**调试**。 你将看到**Run64BitRuntime**下的属性**调试选项**。 若要使用 32 位运行时，将其设置为**False**。 若要使用 64 位运行时，将其设置为**True**。  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>运行从 SQL Server 2012 SQL Server 数据工具  
若要运行 SQL Server Data Tools 中的从包，右键单击你的包，然后选择**执行包**。  
  
### <a name="run-from-powershell"></a>从 PowerShell 中运行  
若要从 Windows PowerShell，运行包使用**dtexec**实用程序： `dtexec /FILE <packagePath>`  
  
例如，使用 IPv4 地址 `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>运行从 Windows 命令提示符 
若要从 Windows 命令提示符，运行包使用**dtexec**实用程序： `dtexec /FILE <packagePath>`  
  
例如： `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>数据类型  
当使用 Integration Services 将数据从数据源加载到 SQL Server PDW 数据库，数据首先映射将源数据中到 Integration Services 数据类型。 这允许来自多个数据源的数据映射到一组通用的数据类型。  
  
然后将数据从 Integration Services 映射到 SQL Server PDW 数据类型。 对于每个 SQL Server PDW 数据类型下, 表列出可以转换为 SQL Server PDW 数据类型的 Integration Services 数据类型。  
  
|PDW 数据类型|映射到 PDW 数据类型的 integration Services 数据类型 (s)|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|bigint|DT_I1、DT_I2、DT_I4、DT_I8、DT_UI1、DT_UI2、DT_UI4|  
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
  
**对数据类型精度的支持有限**  
  
如果映射 DT_NUMERIC 或 DT_DECIMAL 输入包含具有精度大于 28 的值的列，PDW 会生成验证错误。  
  
**不支持的数据类型**  
  
SQL Server PDW 不支持以下 Integration Services 数据类型：  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
若要加载到 SQL Server PDW 中包含的这些类型的数据列，你必须将数据转换转换上游添加数据流将数据转换为兼容的数据类型。  
  
## <a name="permissions"></a>权限  
若要运行 Integration Services 加载包，你需要：  
  
-   加载对数据库拥有权限。  
  
-   适用的插入、 更新对目标表的删除权限。  
  
-   如果使用临时数据库，则将在临时数据库的创建权限。 这是用于创建临时表。  
  
-   如果不使用任何临时数据库，则在目标数据库上的创建权限。 这是用于创建临时表。  
  
## <a name="GenRemarks"></a>常规备注  
当 Integration Services 包已运行的多个 SQL Server PDW 目标，并且其中一个连接已被终止时，则会停止 Integration Services 将数据推送到每个 SQL Server PDW 目标。  
  
## <a name="Limits"></a>限制和局限  
Integration Services 包，同一数据源的 SQL Server PDW 目标数由 active 负载的最大数目限制。 该最大值是预先配置的，用户不可配置。 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
运行包时，同一数据源每个 Integration Services 包目标将计为一个负载。 例如，假定处于活动状态的加载的最大数目为 10。 如果该包尝试为相同数据源打开 11 个或更多的目标，则该包将不运行。  
  
多个包可以同时运行，只要每个包所使用的处于活动状态的加载数目未超过该最大数目。 例如，如果处于活动状态的加载的最大数目为 10，则您可以同时运行两个包，每个包使用 10 个目标。 在一个包运行时，另一个包在加载队列中等待。  
  
如果加载队列中加载的数目超过排队的最大加载数，则该包将不运行。 例如，如果负载的最大数量是每个应用装置的 10 的最大排队加载数为每个应用装置 40，你可以同时运行五个 Integration Services 包的每个打开 10 目标。 如果您尝试运行第 6 个包，该包将不会运行。  

> [!IMPORTANT]
> 如果源表包含与 SQL 排序规则的 char 和 varchar 列，则使用了 PDW 目标适配器的 SSIS 中的 OLE DB 数据源，会导致数据损坏。 我们建议使用 ADO.NET 源，如果源表包含与 SQL 排序规则的 char 或 varchar 列。 

  
## <a name="Locks"></a>锁定行为  
在加载时使用 Integration Services 的数据，SQL ServerPDW 将使用行级锁来更新目标表中的数据。 这意味着，在更新每一行时，对于读取和写入操作，将锁定每一行。 在数据加载到临时表中时，将不锁定目标表中的行。  
  
## <a name="Examples"></a>示例  
  
### <a name="Walkthrough"></a>一个。 从平面文件的简单负载  
下面的演练演示如何使用 Integration Services 来加载到 SQL Server PDW 设备的平面文件数据的简单数据负载。  此示例假定已在客户端计算机上安装集成服务，并已安装 SQL Server PDW 目标，如上面所述。  
  
在此示例中我们将加载到`Orders`具有以下 DDL 的表。 `Orders`表属于`LoadExampleDB`数据库。  
  
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
  
在负载的准备，创建平面文件`exampleLoad.txt`，包含加载数据：  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
首先，创建 Integration Services 包，通过执行下列步骤：  
  
1.  SQL Server Data Tools 中\(SSDT\)，选择**文件**，**新建**，，然后**项目**。 选择**Integration Services 项目**从列出的选项。 将此项目`ExampleLoad`，然后单击**确定**。  
  
2.  单击**控制流**选项卡，然后将**数据流任务**从**工具箱**到**控制流**窗格。  
  
3.  单击**数据流**选项卡，然后将**平面文件源**从**工具箱**到**数据流**窗格。 双击刚创建以打开框**平面文件源编辑器**。  
  
4.  单击**连接管理器**，然后单击**新建**。  
  
5.  在**连接管理器名称**框中，输入连接的友好名称。 对于此示例， `Example Load Flat File CM`。  
  
6.  单击**浏览**和选择`ExampleLoad.txt`从本地计算机的文件。  
  
7.  由于平面文件包含具有列名称的行，请单击**中第一个数据行的列名称**框。  
  
8.  单击**列**左侧的列和预览中的数据将加载以确保列名称和数据已正确解释。  
  
9. 单击**高级**左侧列中。 单击每个列名称来查看已经与数据相关联的数据类型。 在框中键入更改，以便加载的数据的数据类型将与目标列类型兼容。  
  
10. 单击**确定**以保存你的连接管理器。  
  
11. 单击**确定**退出**平面文件源编辑器**。  
  
指定数据流的目标。  
  
1.  拖动**SQL Server PDW 目标**从**工具箱**到**数据流**窗格。  
  
2.  双击刚创建加载框**SQL Server PDW 目标编辑器**。  
  
3.  单击向下箭头旁边**连接管理器**。  
  
4.  选择**创建新的连接**。  
  
5.  填写服务器、 用户、 密码和目标数据库的信息特定于你的设备的信息。 （示例所示）。 再单击 **“确定”**。  
  
    对于 InfiniBand 连接，**服务器名称**： 输入 < 设备-名称 >-SQLCTL01，17001。  
  
    为以太网连接**服务器名称**： 输入控件节点群集、 逗号、 端口 17001 的 IP 地址。 例如，10.192.63.134,17001。  
  
    **用户：**`user1`  
  
    **密码：**`password1`  
  
    **目标数据库：**`LoadExampleDB`  
  
6.  选择的目标表： `Orders`。  
  
7.  选择**追加**作为加载模式，然后单击**确定**。  
  
指定数据流从源到目标。  
  
1.  上**数据流**窗格中，将从绿色箭头拖**平面文件源**到框中**SQL Server PDW 目标**框。  
  
2.  双击**SQL Server PDW 目标**框中，这样您看到**SQL Server PDW 目标编辑器**试。 你应看到在左侧，平面文件中的列名称下**未映射的输入列**。 你应看到来自目标表的列名称在右侧下,**未映射的目标列**。 通过拖动或双击中匹配的列名称映射列**未映射的输入列**和**未映射的目标列**还列出了**映射的列**框。 单击**确定**以保存设置。  
  
3.  通过单击保存包**保存**中**文件**菜单。  
  
Integration Services 在计算机上运行的包。  
  
1.  Integration Services 中**解决方案资源管理器**（右列） 中，右键单击`Package.dtsx`和选择**执行**。  
  
2.  包的运行时间以及上将显示进度以及任何错误**进度**窗格。 使用 SQL 客户端以确认负载，或监视 SQL Server PDW 管理员控制台通过负载。  
  
## <a name="see-also"></a>请参阅  
[创建使用 SSIS PDW 目标适配器的脚本任务](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](http://msdn.microsoft.com/library/ms141026\(v=sql11\).aspx)  
[设计和实现包 (Integration Services)](http://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[教程： 创建基本包使用向导](http://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[入门 (Integration Services)](http://go.microsoft.com/fwlink/?LinkId=202412)  
[动态包生成示例](http://go.microsoft.com/fwlink/?LinkId=202413)  
[为并行度 （SQL Server 视频） 设计 SSIS 包](http://msdn.microsoft.com/library/dd795221.aspx)  
[Microsoft SQL Server 社区示例： Integration Services](http://go.microsoft.com/fwlink/?LinkId=202415)  
[与变更数据捕获改善增量加载](http://msdn.microsoft.com/library/bb895315\(v=sql11\).aspx)  
[渐变维度转换](http://msdn.microsoft.com/library/ms141715\(v=sql11\).aspx)  
[大容量插入任务](http://msdn.microsoft.com/library/ms141239\(v=sql11\).aspx)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
