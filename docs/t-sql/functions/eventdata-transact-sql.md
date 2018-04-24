---
title: EVENTDATA (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- EVENTDATA
- fn_event_data
- EVENTDATA_TSQL
- fn_event_data_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server instance event data [SQL Server]
- event notifications [SQL Server], event status
- events [SQL Server], status infromation
- EVENTDATA function
- status information [SQL Server], events
- DDL triggers, returning event data
ms.assetid: 03a80e63-6f37-4b49-bf13-dc35cfe46c44
caps.latest.revision: 55
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a1bee1eccc84c6938ff1fccb1343dd24284769c2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="eventdata-transact-sql"></a>EVENTDATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回有关服务器或数据库事件的信息。 激发事件通知时将调用 EVENTDATA，并且结果返回到指定的 Service Broker。 还可以在 DDL 或登录触发器正文的内部使用 EVENTDATA。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
EVENTDATA( )  
```  
  
## <a name="remarks"></a>Remarks  
 只有直接在 DDL 或登录触发器内部引用 EVENTDATA 时，EVENTDATA 才会返回数据。 如果 EVENTDATA 由其他例程调用（即使这些例程由 DDL 或登录触发器进行调用），将返回 NULL。  
  
 在隐式或显式调用 EVENTDATA 的事务提交或回滚之后，EVENTDATA 所返回的数据将无效。  
  
> [!CAUTION]  
>  EVENTDATA 返回 XML 数据。 该数据将以 Unicode 的形式（其中每个字符包含 2 个字节）发送到客户端。 以下 Unicode 码位可以在 EVENTDATA 所返回的 XML 中使用：  
>   
>  `0x0009`  
>   
>  `0x000A`  
>   
>  `0x000D`  
>   
>  `>= 0x0020 && <= 0xD7FF`  
>   
>  `>= 0xE000 && <= 0xFFFD`  
>   
>  某些可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 标识符和数据中使用的字符不能或不允许在 XML 中使用。 其码位没有显示在前面列表中的字符或数据将映射为问号 (?)。  
  
 为了保护登录名的安全性，当执行 CREATE LOGIN 或 ALTER LOGIN 语句时，将不显示密码。  
  
## <a name="schemas-returned"></a>返回的架构  
 EVENTDATA 返回类型为 xml 的值。 默认情况下，所有事件的架构定义都安装在以下目录中：[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd。  
  
 此外，事件架构还发布在 [Microsoft SQL Server XML 架构](http://go.microsoft.com/fwlink/?LinkID=31850)网页。  
  
 若要提取任何特定事件的架构，请搜索复杂类型 `EVENT_INSTANCE_\<event_type>` 的架构。 例如，若要提取 DROP_TABLE 事件的架构，请搜索 `EVENT_INSTANCE_DROP_TABLE` 的架构。  
  
## <a name="examples"></a>示例  
  
### <a name="a-querying-event-data-in-a-ddl-trigger"></a>A. 在 DDL 触发器中查询事件数据  
 以下示例创建 DDL 触发器，以防止在数据库中创建新表。 通过对 EVENTDATA 生成的 XML 数据使用 XQuery，可以捕获激发触发器的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 有关详细信息，请参阅 [XQuery 语言参考 (SQL Server)](../../xquery/xquery-language-reference-sql-server.md)。  
  
> [!NOTE]  
>  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的“以网格显示结果”来查询 `\<TSQLCommand>` 元素时，命令文本中的分行符不会出现。 请改用“以文本格式显示结果”。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value  
        ('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
GO  
--Test the trigger.  
CREATE TABLE NewTable (Column1 int);  
GO  
--Drop the trigger.  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
> [!NOTE]  
>  如果需要返回事件数据，建议使用 XQuery value() 方法而不是 query() 方法。 query() 方法可在输出中返回 XML 和以“and”符转义的回车符和换行符 (CR/LF) 实例，而 value() 方法无法在输出中呈现 CR/LF 实例。  
  
### <a name="b-creating-a-log-table-with-event-data-in-a-ddl-trigger"></a>B. 创建事件数据在 DDL 触发器中的日志表  
 以下示例创建用于存储所有数据库级事件的相关信息的表，并在表中填充 DDL 触发器。 通过对 `EVENTDATA` 生成的 XML 数据使用 XQuery，可以捕获事件类型和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE ddl_log (PostTime datetime, DB_User nvarchar(100), Event nvarchar(100), TSQL nvarchar(2000));  
GO  
CREATE TRIGGER log   
ON DATABASE   
FOR DDL_DATABASE_LEVEL_EVENTS   
AS  
DECLARE @data XML  
SET @data = EVENTDATA()  
INSERT ddl_log   
   (PostTime, DB_User, Event, TSQL)   
   VALUES   
   (GETDATE(),   
   CONVERT(nvarchar(100), CURRENT_USER),   
   @data.value('(/EVENT_INSTANCE/EventType)[1]', 'nvarchar(100)'),   
   @data.value('(/EVENT_INSTANCE/TSQLCommand)[1]', 'nvarchar(2000)') ) ;  
GO  
--Test the trigger.  
CREATE TABLE TestTable (a int);  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
--Drop the trigger.  
DROP TRIGGER log  
ON DATABASE;  
GO  
--Drop table ddl_log.  
DROP TABLE ddl_log;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用 EVENTDATA 函数](../../relational-databases/triggers/use-the-eventdata-function.md)   
 [DDL 触发器](../../relational-databases/triggers/ddl-triggers.md)   
 [事件通知](../../relational-databases/service-broker/event-notifications.md)   
 [登录触发器](../../relational-databases/triggers/logon-triggers.md)  
  
  
