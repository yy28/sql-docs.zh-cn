---
title: "使用 SQL Server Profiler 创建和测试计划指南 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-plan-guides"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "检查计划指南"
  - "计划指南 [SQL Server], 测试"
  - "计划指南 [SQL Server], SQL Server Profiler"
  - "将查询与计划指南匹配 [SQL Server]"
  - "测试计划指南"
  - "SQL Server Profiler, 计划指南"
  - "计划指南 [SQL Server], 创建"
  - "捕获查询文本 [SQL Server]"
  - "验证计划指南"
  - "Profiler [SQL Server Profiler], 计划指南"
  - "查询与计划指南相匹配 [SQL Server]"
ms.assetid: 7018dbf0-1a1a-411a-88af-327bedf9cfbd
caps.latest.revision: 31
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 31
---
# 使用 SQL Server Profiler 创建和测试计划指南
  在创建计划指南时，可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 来捕获完全匹配的查询文本，以供 **sp_create_plan_guide** 存储过程的 *statement_text* 参数使用。 这有助于确保计划指南在编译时与查询匹配。 创建计划指南后，还可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 来测试计划指南是否确实与查询匹配。 通常，应使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 来验证查询是否与计划指南匹配，从而测试计划指南。  
  
## 使用 SQL Server Profiler 捕获查询文本  
 如果执行了查询，并使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 捕获到与提交到 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]时完全相同的文本，则可以创建完全匹配查询文本的 SQL 或 TEMPLATE 类型的计划指南。 这将确保计划指南可由查询优化器使用。  
  
 思考以下作为独立批处理由应用程序提交的查询：  
  
```  
SELECT COUNT(*) AS c  
FROM Sales.SalesOrderHeader AS h  
INNER JOIN Sales.SalesOrderDetail AS d  
  ON h.SalesOrderID = d.SalesOrderID  
WHERE h.OrderDate BETWEEN '20000101' and '20050101';  
```  
  
 假设您要通过合并联接操作执行此查询，但 SHOWPLAN 指示该查询未使用合并联接。 因为无法在应用程序中直接更改查询，所以可以改为创建计划指南来指定在编译时将 MERGE JOIN 查询提示追加到该查询。  
  
 若要捕获与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接收时完全相同的查询文本，请执行以下步骤：  
  
1.  启动 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 跟踪，确保已选中 **SQL:BatchStarting** 事件类型。  
  
2.  使应用程序运行查询。  
  
3.  暂停 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 跟踪。  
  
4.  单击与该查询对应的 **SQL:BatchStarting** 事件。  
  
5.  右键单击并选择“提取事件数据”。  
  
    > [!IMPORTANT]  
    >  不要尝试通过从事件探查器跟踪窗口的下窗格中选中批处理文本来复制它。 这可能会导致所创建的计划指南与原始批处理不匹配。  
  
6.  将事件数据保存到文件。 这就是批处理文本。  
  
7.  在记事本中打开该批处理文本文件，将文本复制到复制和粘贴缓冲区。  
  
8.  创建计划指南，并将复制的文本粘贴到为 **@stmt** 参数指定的引号 (**''**) 内。 必须通过在前面再加上其他单引号来转义 **@stmt** 参数中的任何单引号。 插入这些单引号时务必小心，不要添加或删除任何其他字符。 例如，日期文本 **'**20000101**'** 必须分隔为 **''**20000101**''**。  
  
 下面是该计划指南：  
  
```  
EXEC sp_create_plan_guide   
    @name = N'MyGuide1',  
    @stmt = N'<paste the text copied from the batch text file here>',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = NULL,  
    @hints = N'OPTION (MERGE JOIN)';  
```  
  
## 使用 SQL Server Profiler 测试计划指南  
 若要验证计划指南是否与查询匹配，请执行以下步骤：  
  
1.  启动 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 跟踪，确保已选中 **Showplan XML** 事件类型（位于“性能”节点下）。  
  
2.  使应用程序运行查询。  
  
3.  暂停 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 跟踪。  
  
4.  在 **Showplan XML** 事件中查找受影响的查询。  
  
    > [!NOTE]  
    >  无法使用 **“查询编译的 Showplan XML”** 事件。 **PlanGuideDB** 在该事件中不存在。  
  
5.  如果计划指南的类型为 OBJECT 或 SQL，则请验证 **Showplan XML** 事件是否包含您希望与查询匹配的计划指南的 **PlanGuideDB** 和 **PlanGuideName** 属性。 或者，如果计划指南的类型为 TEMPLATE，则请验证 **Showplan XML** 事件是否包含预期计划指南的 **TemplatePlanGuideDB** 和 **TemplatePlanGuideName** 属性。 这可以验证计划指南是否在运行。 这些属性包含在计划的 **\<StmtSimple>** 元素下。  
  
## 另请参阅  
 [sp_create_plan_guide (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
  
  