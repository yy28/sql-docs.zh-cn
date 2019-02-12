---
title: 基于文本的查询设计器用户界面 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10010"
- sql12.rtp.rptdesigner.dataview.genericquerydesigner.f1
helpviewer_keywords:
- text-based query designer [Reporting Services]
- query designers [Reporting Services], text-based
ms.assetid: 44b7c664-03aa-494e-a484-052b318e810c
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 61c57d661a9865c9ced6912af921dd45b9e1db74
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012388"
---
# <a name="text-based-query-designer-user-interface"></a>基于文本的查询设计器用户界面
  使用基于文本的查询设计器可以用数据源支持的查询语言来指定查询，还可以运行查询并在运行时查看结果。 您可以指定多个 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句，为自定义数据处理扩展插件指定查询或命令语法，还可以指定指定为表达式的查询。 因为基于文本的查询设计器不会对查询进行预处理，并且能适应任何类型的查询语法，所以成为了众多数据源类型的默认查询设计器工具。  
  
 基于文本的查询设计器将显示工具栏和以下两个窗格：  
  
-   **查询**显示查询文本、 表名或存储的过程的名称。  
  
-   **结果** ：在设计时，显示查询的运行结果。  
  
## <a name="text-based-query-designer-toolbar"></a>基于文本的查询设计器工具栏  
 基于文本的查询设计器为所有命令类型都提供一个单一工具栏。 下表列出了该工具栏中的每个按钮及其功能。  
  
|Button|Description|  
|------------|-----------------|  
|**编辑为文本**|在基于文本的查询设计器和图形查询设计器之间切换。 并非所有的数据源类型都支持图形查询设计器。|  
|**导入**|从文件或报表中导入现有的查询。 仅支持 .sql 和 .rdl 文件类型。 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。|  
|![运行查询](../analysis-services/media/rsqdicon-run.gif "运行查询")|运行查询并在“结果”窗格中显示结果集。|  
|**命令类型**|选择 **Text**、 **StoredProcedure**或 **TableDirect**。 如果存储过程带有参数，则单击工具栏上的 **“运行”** 时，将出现 **“定义查询参数”** 对话框，您可以根据需要填入值。 请注意，是否存储的过程返回多个结果集，只将第一个结果集用于填充数据集。<br /><br /> 所支持的命令类型因数据源类型而异。 例如，仅 OLE DB 和 ODBC 支持 **TableDirect**。|  
  
### <a name="command-type-text"></a>命令类型 Text  
 创建 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据集时，默认情况下，报表设计器会显示图形查询设计器。 若要切换为基于文本的查询设计器，请单击工具栏上的“编辑为文本”切换按钮。 基于文本的查询设计器将显示两个窗格：“查询”窗格和“结果”窗格。 下图标出了每个窗格。  
  
 ![通用查询设计器，用于关系数据查询](../analysis-services/media/rsqd-dsaw-sql-generic.gif "通用查询设计器，用于关系数据查询")  
  
 下表介绍了每个窗格的功能。  
  
|Pane|函数|  
|----------|--------------|  
|查询|显示 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询文本。 使用此窗格可以编写或编辑 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询。|  
|结果|显示查询的结果。 若要运行查询，请右键单击任意窗格，然后单击“运行”，或者单击工具栏中的“运行”按钮。|  
  
#### <a name="example"></a>示例  
 以下查询将从 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库的 `Contact` 表中返回姓氏列表：  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 您可以对命令类型文本使用任何 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句，包括 `EXEC` 语句。 以下查询将调用[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]存储过程`uspGetEmployeeManagers`，并为标识号为 1 的雇员返回命令链。  
  
```  
EXEC uspGetEmployeeManagers 1;  
```  
  
 单击工具栏上的 **“运行”** 时，将运行 **“查询”** 窗格中的命令，并在 **“结果”** 窗格中显示结果。  
  
### <a name="command-type-storedprocedure"></a>命令类型 StoredProcedure  
 选择“Command typeStoredProcedure”时，基于文本的查询设计器将显示两个窗格：“查询”窗格和“结果”窗格。 在“查询”窗格中输入存储过程的名称，然后单击工具栏中的 **“运行”** 按钮。 此时将打开“定义查询参数”对话框。 输入存储过程的参数值。 对于每个存储过程参数，都会创建一个报表参数。  
  
#### <a name="example"></a>示例  
 以下查询调用 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 存储过程 `uspGetEmployeeManagers`。 您必须在运行查询时，为雇员标识号参数输入值。  
  
```  
uspGetEmployeeManagers;  
```  
  
### <a name="command-type-tabledirect"></a>命令类型 TableDirect  
 选择“Command typeTableDirect”时，基于文本的查询设计器将显示两个窗格：“查询”窗格和“结果”窗格。 如果输入一个表并单击 **“运行”** 按钮，则将返回该表的所有列。  
  
#### <a name="example"></a>示例  
 以下查询将返回 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库中的所有客户的结果集。  
  
 `Sales.Customer`  
  
 如果输入表名 Sales.Customer，则创建的等同[!INCLUDE[tsql](../includes/tsql-md.md)]语句`SELECT * FROM Sales.Customer;`。  
  
## <a name="see-also"></a>请参阅  
 [查询设计工具在报表设计器的 SQL Server Data Tools &#40;SSRS&#41;](report-data/query-design-tools-ssrs.md)   
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [SQL Server 连接类型 (SSRS)](report-data/sql-server-connection-type-ssrs.md)   
 [OLE DB 连接类型 (SSRS)](report-data/ole-db-connection-type-ssrs.md)   
 [ODBC 连接类型&#40;SSRS&#41;](report-data/odbc-connection-type-ssrs.md)   
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [RSReportDesigner 配置文件](report-server/rsreportdesigner-configuration-file.md)  
  
  
