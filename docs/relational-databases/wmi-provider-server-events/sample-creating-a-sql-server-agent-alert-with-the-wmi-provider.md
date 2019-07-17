---
title: 示例：使用 WMI 提供程序创建 SQL Server 代理警报 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SQL Server Agent [WMI]
- WMI Provider for Server Events, samples
- sample applications [WMI]
ms.assetid: d44811c7-cd46-4017-b284-c863ca088e8f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 875751bd4b2dffd0039ffb40aa884bb9731a75d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139494"
---
# <a name="sample-creating-a-sql-server-agent-alert-with-the-wmi-provider"></a>示例：使用 WMI 提供程序创建 SQL Server 代理警报
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  WMI 事件提供程序的一个常见用法是创建响应特定事件的 SQL Server 代理警报。 以下示例提供一个在表中保存 XML 死锁图形事件以供以后分析的简单警报。 SQL Server 代理提交 WQL 请求、接收 WMI 事件并运行作业以响应该事件。 请注意，尽管在处理通知消息中涉及几个 Service Broker 对象，WMI 事件提供程序将处理创建和管理这些对象的详细信息。  
  
## <a name="example"></a>示例  
 首先，在 `AdventureWorks` 数据库中创建一个表来存放死锁图形事件。 该表包含两个列：`AlertTime`列包含警报所运行的时间和`DeadlockGraph`列包含的 XML 文档中包含的死锁图形。  
  
 然后，创建警报。 脚本首先创建将运行警报的作业，将作业步骤添加到作业，然后指定作业目标为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的当前实例。 然后，脚本创建警报。  
  
 作业步骤检索**TextData**属性的 WMI 事件实例并将该值插入**DeadlockGraph**的列**DeadlockEvents**表。 请注意，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将该字符串隐式转换为 XML 格式。 因为作业步骤使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 子系统，因此它不指定代理。  
  
 每当记录死锁图形跟踪事件时，警报都将运行该作业。 对于 WMI 警报，SQL Server 代理使用指定的命名空间和 WQL 语句创建一个通知查询。 对于此警报，SQL Server 代理监视本地计算机上的默认实例。 WQL 语句请求默认实例中的任何 `DEADLOCK_GRAPH` 事件。 若要更改警报监视的实例，请替换该警报的 `MSSQLSERVER` 中 `@wmi_namespace` 的实例名称。  
  
> [!NOTE]  
>  SQL Server 代理以接收 WMI 事件[!INCLUDE[ssSB](../../includes/sssb-md.md)]必须在中启用**msdb**和[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]。  
  
```  
USE AdventureWorks ;  
GO  
  
IF OBJECT_ID('DeadlockEvents', 'U') IS NOT NULL  
BEGIN  
    DROP TABLE DeadlockEvents ;  
END ;  
GO  
  
CREATE TABLE DeadlockEvents  
    (AlertTime DATETIME, DeadlockGraph XML) ;  
GO  
-- Add a job for the alert to run.  
  
EXEC  msdb.dbo.sp_add_job @job_name=N'Capture Deadlock Graph',   
    @enabled=1,   
    @description=N'Job for responding to DEADLOCK_GRAPH events' ;  
GO  
  
-- Add a jobstep that inserts the current time and the deadlock graph into  
-- the DeadlockEvents table.  
  
EXEC msdb.dbo.sp_add_jobstep  
    @job_name = N'Capture Deadlock Graph',  
    @step_name=N'Insert graph into LogEvents',  
    @step_id=1,   
    @on_success_action=1,   
    @on_fail_action=2,   
    @subsystem=N'TSQL',   
    @command= N'INSERT INTO DeadlockEvents  
                (AlertTime, DeadlockGraph)  
                VALUES (getdate(), N''$(ESCAPE_SQUOTE(WMI(TextData)))'')',  
    @database_name=N'AdventureWorks' ;  
GO  
  
-- Set the job server for the job to the current instance of SQL Server.  
  
EXEC msdb.dbo.sp_add_jobserver @job_name = N'Capture Deadlock Graph' ;  
GO  
  
-- Add an alert that responds to all DEADLOCK_GRAPH events for  
-- the default instance. To monitor deadlocks for a different instance,  
-- change MSSQLSERVER to the name of the instance.  
  
EXEC msdb.dbo.sp_add_alert @name=N'Respond to DEADLOCK_GRAPH',   
@wmi_namespace=N'\\.\root\Microsoft\SqlServer\ServerEvents\MSSQLSERVER',   
    @wmi_query=N'SELECT * FROM DEADLOCK_GRAPH',   
    @job_name='Capture Deadlock Graph' ;  
GO  
```  
  
## <a name="testing-the-sample"></a>测试示例  
 若要查看作业运行情况，请造成死锁。 在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，打开两个**SQL 查询**选项卡，然后连接到同一个实例的两个查询。 在其中一个查询选项卡中运行以下脚本。 此脚本生成一个结果集，然后结束。  
  
```  
USE AdventureWorks ;  
GO  
  
BEGIN TRANSACTION ;  
GO  
  
SELECT TOP(1) Name FROM Production.Product WITH (XLOCK) ;  
GO  
```  
  
 在第二个查询选项卡中运行以下脚本。此脚本生成一个结果集，然后被阻塞，等待上获取锁`Production.Product`。  
  
```  
USE AdventureWorks ;  
GO  
  
BEGIN TRANSACTION ;  
GO  
  
SELECT TOP(1) Name FROM Production.Location WITH (XLOCK) ;  
GO  
  
SELECT TOP(1) Name FROM Production.Product WITH (XLOCK) ;  
GO  
```  
  
 在第一个查询选项卡中运行以下脚本。此脚本被阻塞，等待上获取锁`Production.Location`。 在很短的超时值过后，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将选择此脚本或示例中的脚本作为死锁牺牲品，然后结束事务。  
  
```  
SELECT TOP(1) Name FROM Production.Location WITH (XLOCK) ;  
GO  
```  
  
 造成死锁后，等待一段时间，以便 SQL Server 代理激活警报并运行作业。 通过运行以下脚本查看 `DeadlockEvents` 表的内容：  
  
```  
SELECT * FROM DeadlockEvents ;  
GO  
```  
  
 `DeadlockGraph` 列应包含显示死锁图形事件的所有属性的 XML 文档。  
  
## <a name="see-also"></a>请参阅  
 [WMI Provider for Server Events 的概念](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
  
  
