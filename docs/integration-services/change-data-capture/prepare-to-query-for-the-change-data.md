---
title: "准备查询变更数据 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- incremental load [Integration Services],preparing query
ms.assetid: 9ea2db7a-3dca-4bbf-9903-cccd2d494b5f
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b15733feeca10976315834b2dfc897cc8a9d1216
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="prepare-to-query-for-the-change-data"></a>准备查询变更数据
  在用于执行变更数据增量加载的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的控制流中，第三个任务（即最后一个任务）是准备查询变更数据和添加数据流任务。  
  
> [!NOTE]  
>  控制流的第二个任务是确保所选间隔的变更数据已准备就绪。 有关此任务的详细信息，请参阅[确定变更数据是否已准备就绪](../../integration-services/change-data-capture/determine-whether-the-change-data-is-ready.md)。 有关设计控制流的总体过程的说明，请参阅[变更数据捕获 (SSIS)](../../integration-services/change-data-capture/change-data-capture-ssis.md)。  
  
## <a name="design-considerations"></a>设计注意事项  
 为了检索变更数据，您将调用 Transact-SQL 表值函数，该函数将间隔的端点接受为输入参数并返回指定间隔的变更数据。 数据流中的源组件调用此函数。 有关此源组件的信息，请参阅 [检索和了解变更数据](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md)。  
  
 最常用的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 源组件（包括 OLE DB 源、ADO 源和 ADO NET 源）无法为表值函数派生参数信息。 因此，大多数源不能直接调用参数化的函数。  
  
 您可以使用以下两个设计选项将输入参数传递到函数：  
  
-   **将参数化查询组合为字符串**。 可以使用脚本任务或执行 SQL 任务将动态的 SQL 字符串与硬编码的参数值组合为字符串。 然后，将该字符串存储在包变量中，并用它来设置源组件的 SqlCommand 属性。 此方法之所以成功，是因为源组件不再需要参数信息。  
  
    > [!NOTE]  
    >  预编译的脚本产生的开销小于执行 SQL 任务。  
  
-   **使用参数化的包装**。 此外，还可以以包装的形式创建一个参数化的存储过程，以调用参数化的表值函数。 此方法之所以成功，是因为源组件可以成功地为存储过程派生参数信息。  
  
 本主题使用第一个设计选项，即将参数化查询组合为字符串。  
  
## <a name="preparing-the-query"></a>准备查询  
 将输入参数的值连接到单个查询字符串中之前，必须设置查询所需的包变量。  
  
#### <a name="to-set-up-package-variables"></a>设置包变量  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的 **“变量”** 窗口中，创建一个数据类型为 string 的变量以保存执行 SQL 任务返回的查询字符串。  
  
     以下示例使用变量名 SqlDataQuery。  
  
 创建包变量后，可以使用脚本任务或执行 SQL 任务连接输入参数的值。 下面的两个过程介绍如何配置这些组件。  
  
#### <a name="to-use-a-script-task-to-concatenate-the-query-string"></a>使用脚本任务连接查询字符串  
  
1.  在 **“控制流”** 选项卡上，在包中的 For 循环容器后添加一个脚本任务，然后将 For 循环容器连接到该任务。  
  
    > [!NOTE]  
    >  此过程假定包从一个表中执行增量加载。 如果包从多个表加载并且具有包含多个子包的父包，则将该任务作为第一个组件添加到各子包中。 有关详细信息，请参阅 [执行多个表的增量加载](../../integration-services/change-data-capture/perform-an-incremental-load-of-multiple-tables.md)。  
  
2.  在 **“脚本任务编辑器”**中的 **“脚本”** 页上，选择以下选项：  
  
    1.  对于 **ReadOnlyVariables**，从列表中选择 **User::DataReady**、 **User::ExtractStartTime**和 **User::ExtractEndTime** 。  
  
    2.  对于 **ReadWriteVariables**，从列表中选择 User::SqlDataQuery。  
  
3.  在 **“脚本任务编辑器”**的 **“脚本”** 页上，单击 **“编辑脚本”** 以打开脚本开发环境。  
  
4.  在 Main 过程中，输入下面的代码段之一：  
  
    -   如果使用 C# 进行编程，请输入下面的代码行：  
  
        ```  
        int dataReady;  
        System.DateTime extractStartTime;  
        System.DateTime extractEndTime;  
        string sqlDataQuery;  
  
        dataReady = (int)Dts.Variables["DataReady"].Value;  
        extractStartTime = (System.DateTime)Dts.Variables["ExtractStartTime"].Value;  
        extractEndTime = (System.DateTime)Dts.Variables["ExtractEndTime"].Value;  
  
        if (dataReady == 2)  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) + "', '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
        else  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" + ", '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
  
        Dts.Variables["SqlDataQuery"].Value = sqlDataQuery;  
        ```  
  
         \- 或 -  
  
    -   如果您是使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]进行编程，请输入下面的代码行：  
  
        ```  
        Dim dataReady As Integer  
        Dim extractStartTime As Date  
        Dim extractEndTime As Date  
        Dim sqlDataQuery As String  
  
        dataReady = CType(Dts.Variables("DataReady").Value, Integer)  
        extractStartTime = CType(Dts.Variables("ExtractStartTime").Value, Date)  
        extractEndTime = CType(Dts.Variables("ExtractEndTime").Value, Date)  
  
        If dataReady = 2 Then  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) & _  
              "', '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        Else  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" & _  
              ", '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        End If  
  
        Dts.Variables("SqlDataQuery").Value = sqlDataQuery  
  
        ```  
  
5.  保留从脚本执行过程返回 **DtsExecResult.Success** 的默认代码行。  
  
6.  关闭脚本开发环境和 **“脚本任务编辑器”**。  
  
#### <a name="to-use-an-execute-sql-task-to-concatenate-the-query-string"></a>使用执行 SQL 任务连接查询字符串  
  
1.  在 **“控制流”** 选项卡上，在 For 循环容器之后向包添加一个执行 SQL 任务，然后将 For 循环容器连接到该任务。  
  
    > [!NOTE]  
    >  此过程假定包从一个表中执行增量加载。 如果包从多个表加载并且具有包含多个子包的父包，则将该任务作为第一个组件添加到各子包中。 有关详细信息，请参阅 [执行多个表的增量加载](../../integration-services/change-data-capture/perform-an-incremental-load-of-multiple-tables.md)。  
  
2.  在 **“执行 SQL 任务编辑器”**中的 **“常规”** 页上，选择以下选项：  
  
    1.  对于 **ResultSet**，选择 **“单行”**。  
  
    2.  配置到源数据库的有效连接。  
  
    3.  对于 **SQLSourceType**，选择 **“直接输入”**。  
  
    4.  对于 **SQLStatement**，输入以下 SQL 语句：  
  
        ```  
        declare @ExtractStartTime datetime,  
        @ExtractEndTime datetime,   
        @DataReady int  
  
        select @DataReady = ?,   
        @ExtractStartTime = ?,   
        @ExtractEndTime = ?  
  
        if @DataReady = 2  
        select N'select * from CDCSample.uf_Customer'  
        + N'('''+ convert(nvarchar(30),@ExtractStartTime,120)  
        + ''', '''  
        + convert(nvarchar(30),@ExtractEndTime,120) + ''') '   
        as SqlDataQuery  
        else  
        select N'select * from CDCSample.uf_Customer'  
        + N'(null, '''  
        + convert(nvarchar(30),@ExtractEndTime,120)  
        + ''') '  
        as SqlDataQuery  
  
        ```  
  
        > [!NOTE]  
        >  上述示例中的 **else** 子句通过为开始日期和时间传递 null 值来生成查询，用于变更数据的首次加载。 此示例没有涉及到一种情况：必须将启用变更数据捕获功能之前所做的变更上传到数据仓库。  
  
3.  在 **“执行 SQL 任务编辑器”** 的 **“参数映射”**页上，进行以下映射：  
  
    1.  将 DataReady 变量映射到参数 0。  
  
    2.  将 ExtractStartTime 变量映射到参数 1。  
  
    3.  将 ExtractEndTime 变量映射到参数 2。  
  
4.  在 **“执行 SQL 任务编辑器”** 的 **“结果集”**页上，将结果名称映射到 SqlDataQuery 变量。  
  
     该结果名称是返回的单列的名称 SqlDataQuery。  
  
 上述过程配置的任务使用输入参数的硬编码字符串值准备查询字符串。 下面的代码是此查询字符串的示例：  
  
 `select * from CDCSample. uf_Customer('2007-06-11 14:21:58', '2007-06-12 14:21:58')`  
  
## <a name="adding-a-data-flow-task"></a>添加数据流任务  
 设计包的控制流的最后一步是添加数据流任务。  
  
#### <a name="to-add-a-data-flow-task-and-complete-the-control-flow"></a>添加数据流任务和完成控制流  
  
-   在 **“控制流”** 选项卡上，添加一个数据流任务，并连接用于连接查询字符串的任务。  
  
## <a name="next-step"></a>下一步  
 在准备查询字符串和配置数据流任务之后，下一步就是创建用于从数据库检索变更数据的表值函数。  
  
 **下一个主题：**[创建函数以检索变更数据](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)  
  
  

