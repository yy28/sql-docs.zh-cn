---
title: "合并的数据事件探查任务在包工作流 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Data Profiling task [Integration Services], using output in workflow
ms.assetid: 39a51586-6977-4c45-b80b-0157a54ad510
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ea3c68e0320216c81ce2a47f426112dd4a25f22f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="incorporate-a-data-profiling-task-in-package-workflow"></a>合并包工作流中的数据事件探查任务
  数据事件探查和清除在其早期阶段不适合作为自动过程。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，通常需要对数据事件探查任务的输出进行直观的分析和人为判断，以确定报告的冲突是有意义还是过多。 即使在确认了数据质量问题之后，仍然需要通过周详的计划来确定执行清除的最佳方法。  
  
 不过，在确定了有关数据质量的条件之后，您可能希望对数据源自动执行定期的分析和清除。 请考虑下面的方案：  
  
-   **在增量加载之前检查数据质量**。 使用数据事件探查任务计算用于 Customers 表 CustomerName 列的新数据的列 Null 比率配置文件。 如果 Null 值的百分比大于 20%，则向操作员发送包含该配置文件输出的电子邮件并结束该包。 否则，请继续执行增量加载。  
  
-   **满足指定条件时自动执行清除**。 使用数据事件探查任务根据省/市/自治区的查找表计算 State 列的值包含配置文件，根据邮政编码的查找表计算 ZIP Code/Postal Code 列的值包含配置文件。 如果 State 值的包含强度小于 80%，但 ZIP Code/Postal Code 值的包含强度大于 99%，则表明两个问题： 首先，State 数据无效。 其次，ZIP Code/Postal Code 数据有效。 启动数据流任务，该任务通过从当前的 Zip Code/Postal Code 值中查找正确的 State 值来清除 State 数据。  
  
 具有可以将数据流任务合并到其中的工作流后，还需要了解添加此任务所需的步骤。 下一部分介绍合并数据流任务的一般过程。 最后两部分介绍如何将数据流任务直接连接到数据源或连接到从该数据流转换的数据。  
  
## <a name="defining-a-general-workflow-for-the-data-flow-task"></a>为数据流任务定义常规工作流  
 下面的过程概述了在包的工作流中使用数据事件探查任务的输出的常规方法。  
  
#### <a name="to-use-the-output-of-the-data-profiling-task-programmatically-in-a-package"></a>在包中以编程的方式使用数据事件探查任务的输出  
  
1.  在包中添加和配置数据事件探查任务。  
  
2.  配置包变量以便保存要从配置文件结果中检索的值。  
  
3.  添加和配置脚本任务。 将脚本任务连接到数据事件探查任务。 在脚本任务中，写入用于从数据事件探查任务的输出文件读取所需值并填充包变量的代码。  
  
4.  在将脚本任务连接到工作流下游分支的优先约束中，写入使用变量值定位工作流的表达式。  
  
 在将数据事件探查任务合并到包的工作流中时，请注意该任务的以下两个功能：  
  
-   **任务输出**。 数据事件探查任务根据 DataProfile.xsd 架构以 XML 格式将输出写入文件或包变量。 因此，如果希望在包的条件工作流中使用配置文件结果，则需要查询该 XML 输出。 您可以方便地使用 Xpath 查询语言查询此 XML 输出。 若要学习此 XML 输出的结构，可以打开一个示例输出文件或打开该架构本身。 若要打开输出文件或架构，可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]、另一个 XML 编辑器或文本编辑器（如记事本）。  
  
    > [!NOTE]  
    >  数据配置文件查看器中显示的某些配置文件结果是不能在输出中直接找到的计算值。 例如，列 Null 比率配置文件的输出包括总行数和包含 Null 值的行数。 您需要查询这两个值，然后计算包含 Null 值的行的百分比，以得到列 Null 比率。  
  
-   **任务输入**。 数据事件探查任务从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中读取输入。 因此，如果要对数据流中已加载并转换的数据进行事件探查，则需要将内存中的数据保存到临时表中。  
  
 以下各部分将应用此常规工作流，以对直接来自外部数据源的数据或从数据流任务转换而来的数据进行事件探查。 这些部分还说明如何处理数据流任务的输入和输出要求。  
  
## <a name="connecting-the-data-profiling-task-directly-to-an-external-data-source"></a>将数据事件探查任务直接连接到外部数据源  
 数据事件探查任务可以对直接来自数据源的数据进行事件探查。  为了举例说明此功能，下面的示例使用数据事件探查任务对 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的 Person.Address 表的列计算列 Null 比率配置文件。 然后，此示例使用脚本任务从输出文件检索结果，并填充可用来定位工作流的包变量。  
  
> [!NOTE]  
>  因为 AddressLine2 列包含 Null 值的比例高，所以选择该列用于此简单示例。  
  
 此示例步骤如下：  
  
-   对连接到外部数据源的连接管理器以及连接到将包含配置文件结果的输出文件的连接管理器进行配置。  
  
-   对将保存数据事件探查任务所需值的包变量进行配置。  
  
-   配置数据事件探查任务以计算列 Null 比率配置文件。  
  
-   配置脚本任务来处理数据事件探查任务的 XML 输出。  
  
-   配置优先约束，这些约束将根据数据事件探查任务的结果控制运行工作流中的哪些下游分支。  
  
### <a name="configure-the-connection-managers"></a>配置连接管理器  
 在本例中，有两种连接管理器：  
  
-   连接到 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 数据库的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 连接管理器。  
  
-   文件连接管理器，该管理器将创建用于保存数据事件探查任务的结果的输出文件。  
  
##### <a name="to-configure-the-connection-managers"></a>配置连接管理器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创建一个新 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  向该包添加一个 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器。 对此连接管理器进行配置，以使用 NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) 并连接到 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的可用实例。  
  
     默认情况下，连接管理器具有以下名称：\<服务器名称 >。AdventureWorks1。  
  
3.  向该包添加一个文件连接管理器。 对此连接管理器进行配置，以便为数据事件探查任务创建输出文件。  
  
     此示例使用文件名 DataProfile1.xml。 默认情况下，该连接管理器与该文件具有相同的名称。  
  
### <a name="configure-the-package-variables"></a>配置包变量  
 此示例使用两个包变量：  
  
-   ProfileConnectionName 变量将文件连接管理器的名称传递给脚本任务。  
  
-   AddressLine2NullRatio 变量将计算得出的此列的 Null 比率从脚本任务传递给包。  
  
##### <a name="to-configure-the-package-variables-that-will-hold-profile-results"></a>对将保存配置文件结果的包变量进行配置  
  
-   在 **“变量”** 窗口中，添加并配置以下两个包变量：  
  
    -   为其中一个变量输入名称 **ProfileConnectionName**，并将此变量的类型设置为 **String**。  
  
    -   为另一个变量输入名称 **AddressLine2NullRatio**，并将此变量的类型设置为 **Double**。  
  
### <a name="configure-the-data-profiling-task"></a>配置数据事件探查任务  
 在以下情况下，必须对数据事件探查任务进行配置：  
  
-   使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器提供的数据作为输入。  
  
-   对输入数据计算列 Null 比率配置文件。  
  
-   将配置文件结果保存到与文件连接管理器关联的文件中。  
  
##### <a name="to-configure-the-data-profiling-task"></a>配置数据事件探查任务  
  
1.  向控制流添加一个数据事件探查任务。  
  
2.  打开 **“数据事件探查任务编辑器”** 以配置该任务。  
  
3.  在该编辑器的 **“常规”** 页上，选择前面配置的文件连接管理器的名称作为 **“目标”**。  
  
4.  在该编辑器的 **“配置文件请求”** 页上，创建新的列 Null 比率配置文件。  
  
5.  在 **“请求属性”** 窗格中，选择前面配置的 **连接管理器作为**ConnectionManager [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 。 然后选择 Person.Address 作为 **TableOrView**。  
  
6.  关闭数据事件探查任务编辑器。  
  
### <a name="configure-the-script-task"></a>配置脚本任务  
 必须对脚本任务进行配置，以便从输出文件检索结果并填充前面配置的包变量。  
  
##### <a name="to-configure-the-script-task"></a>配置脚本任务  
  
1.  向控制流添加一个脚本任务。  
  
2.  将脚本任务连接到数据事件探查任务。  
  
3.  打开 **“脚本任务编辑器”** 以配置该任务。  
  
4.  在 **“脚本”** 页上，选择首选编程语言。 然后，使两个包变量对该脚本可用：  
  
    1.  对于 **ReadOnlyVariables**，请选择 **ProfileConnectionName**。  
  
    2.  对于 **ReadWriteVariables**，请选择 **AddressLine2NullRatio**。  
  
5.  选择 **“编辑脚本”** 以打开脚本开发环境。  
  
6.  添加对 System.Xml 命名空间的引用。  
  
7.  输入与您的编程语言对应的示例代码：  
  
    ```vb  
    Imports System  
    Imports Microsoft.SqlServer.Dts.Runtime  
    Imports System.Xml  
  
    Public Class ScriptMain  
  
      Private FILENAME As String = "C:\ TEMP\DataProfile1.xml"  
      Private PROFILE_NAMESPACE_URI As String = "http://schemas.microsoft.com/DataDebugger/"  
      Private NULLCOUNT_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()"  
      Private TABLE_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table"  
  
      Public Sub Main()  
  
        Dim profileConnectionName As String  
        Dim profilePath As String  
        Dim profileOutput As New XmlDocument  
        Dim profileNSM As XmlNamespaceManager  
        Dim nullCountNode As XmlNode  
        Dim nullCount As Integer  
        Dim tableNode As XmlNode  
        Dim rowCount As Integer  
        Dim nullRatio As Double  
  
        ' Open output file.  
        profileConnectionName = Dts.Variables("ProfileConnectionName").Value.ToString()  
        profilePath = Dts.Connections(profileConnectionName).ConnectionString  
        profileOutput.Load(profilePath)  
        profileNSM = New XmlNamespaceManager(profileOutput.NameTable)  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI)  
  
        ' Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM)  
        nullCount = CType(nullCountNode.Value, Integer)  
  
        ' Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM)  
        rowCount = CType(tableNode.Attributes("RowCount").Value, Integer)  
  
        ' Compute and return null ratio.  
        nullRatio = nullCount / rowCount  
        Dts.Variables("AddressLine2NullRatio").Value = nullRatio  
  
        Dts.TaskResult = Dts.Results.Success  
  
      End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System;  
    using Microsoft.SqlServer.Dts.Runtime;  
    using System.Xml;  
  
    public class ScriptMain  
    {  
  
      private string FILENAME = "C:\\ TEMP\\DataProfile1.xml";  
      private string PROFILE_NAMESPACE_URI = "http://schemas.microsoft.com/DataDebugger/";  
      private string NULLCOUNT_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()";  
      private string TABLE_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table";  
  
      public void Main()  
      {  
  
        string profileConnectionName;  
        string profilePath;  
        XmlDocument profileOutput = new XmlDocument();  
        XmlNamespaceManager profileNSM;  
        XmlNode nullCountNode;  
        int nullCount;  
        XmlNode tableNode;  
        int rowCount;  
        double nullRatio;  
  
        // Open output file.  
        profileConnectionName = Dts.Variables["ProfileConnectionName"].Value.ToString();  
        profilePath = Dts.Connections[profileConnectionName].ConnectionString;  
        profileOutput.Load(profilePath);  
        profileNSM = new XmlNamespaceManager(profileOutput.NameTable);  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI);  
  
        // Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM);  
        nullCount = (int)nullCountNode.Value;  
  
        // Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM);  
        rowCount = (int)tableNode.Attributes["RowCount"].Value;  
  
        // Compute and return null ratio.  
        nullRatio = nullCount / rowCount;  
        Dts.Variables["AddressLine2NullRatio"].Value = nullRatio;  
  
        Dts.TaskResult = Dts.Results.Success;  
  
      }  
  
    }  
    ```  
  
    > [!NOTE]  
    >  此过程中显示的示例代码说明如何从文件加载数据事件探查任务的输出。 若要从包变量加载数据事件探查任务的输出，请参阅此过程后面的替代示例代码。  
  
8.  关闭脚本开发环境，然后关闭脚本任务编辑器。  
  
#### <a name="alternative-codereading-the-profile-output-from-a-variable"></a>替代代码 - 从变量读取配置文件输出  
 前面的过程显示如何从文件加载数据事件探查任务的输出。 不过，还有一种方法是从包变量加载此输出。 若要从变量加载输出，必须对示例代码进行以下更改：  
  
-   调用 **LoadXml** 类的 **XmlDocument** 方法而不是 **Load** 方法。  
  
-   在脚本任务编辑器中，将包含配置文件输出的包变量的名称添加到该任务的 **ReadOnlyVariables** 列表中。  
  
-   将该变量的字符串值传递给 **LoadXML** 方法，如下面的代码示例所示。 （本示例使用“ProfileOutput”作为包含配置文件输出的包变量的名称。）  
  
    ```vb  
    Dim outputString As String  
    outputString = Dts.Variables("ProfileOutput").Value.ToString()  
    ...  
    profileOutput.LoadXml(outputString)  
    ```  
  
    ```csharp  
    string outputString;  
    outputString = Dts.Variables["ProfileOutput"].Value.ToString();  
    ...  
    profileOutput.LoadXml(outputString);  
    ```  
  
### <a name="configure-the-precedence-constraints"></a>配置优先约束  
 必须对优先约束进行配置，以便根据数据事件探查任务的结果控制运行工作流中的哪些下游分支。  
  
##### <a name="to-configure-the-precedence-constraints"></a>配置优先约束  
  
-   在将脚本任务连接到工作流下游分支的优先约束中，写入使用变量值定位工作流的表达式。  
  
     例如，可以将优先约束的 **“求值运算”** 设置为 **“表达式和约束”**。 然后，可以使用 `@AddressLine2NullRatio < .90` 作为该表达式的值。 当前面的任务成功并且所选列的 Null 值的百分比小于 90% 时，这将使工作流遵循所选的路径。  
  
## <a name="connecting-the-data-profiling-task-to-transformed-data-from-the-data-flow"></a>将数据事件探查任务连接到从数据流转换的数据  
 您可以不对直接来自数据源的数据进行事件探查，而是对数据流中已加载并转换的数据进行事件探查。 不过，数据事件探查任务仅针对持久化数据而不针对内存中的数据进行操作。 因此，必须首先使用目标组件将已转换的数据保存到临时表中。  
  
> [!NOTE]  
>  在配置数据事件探查任务时，必须选择现有表和列。 因此必须在设计时创建临时表，才能配置该任务。 也就是说，此方案不允许使用在运行时创建的临时表。  
  
 将数据保存到临时表中后，即可执行以下操作：  
  
-   使用数据事件探查任务对数据进行事件探查。  
  
-   按照本主题前面所述使用脚本任务读取结果。  
  
-   使用这些结果定位包的后续工作流。  
  
 下面的过程介绍使用数据事件探查任务对已由数据流转换的数据进行事件探查的常规方法。 其中的很多步骤与前面介绍的对直接来自外部数据源的数据进行事件探查的步骤类似。 您可能需要查看前面的这些步骤，以便了解如何配置各种组件的更多信息。  
  
#### <a name="to-use-the-data-profiling-task-in-the-data-flow"></a>在数据流中使用数据事件探查任务  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创建一个包。  
  
2.  在数据流中，添加、配置并连接相应的源和转换。  
  
3.  在数据流中，添加、配置并连接将已转换的数据保存到临时表的目标组件。  
  
4.  在控制流中，添加并配置数据事件探查任务，该任务将根据临时表中的已转换数据计算所需的配置文件。 将数据事件探查任务连接到数据流任务。  
  
5.  配置包变量以便保存要从配置文件结果中检索的值。  
  
6.  添加和配置脚本任务。 将脚本任务连接到数据事件探查任务。 在脚本任务中，写入用于从数据事件探查任务的输出文件读取所需值并填充包变量的代码。  
  
7.  在将脚本任务连接到工作流下游分支的优先约束中，写入使用变量值定位工作流的表达式。  
  
## <a name="see-also"></a>另请参阅  
 [设置数据事件探查任务](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)   
 [数据配置文件查看器](../../integration-services/control-flow/data-profile-viewer.md)  
  
  

