---
ms.openlocfilehash: 6fd7bb2b8be38becc87c4dc8cb353594459a8dd6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68220168"
---

<!--
### Code examples for Azure cloud differ slightly from on-premises
  Or.....
### Code examples can differ for Azure SQL Database
-->

为本地 SQL Server 编写的一些 Transact-SQL 代码示例需要少量更改才能在云中的 Azure SQL 数据库服务上运行。 此类代码示例的一个类别涉及其名称前缀在两个数据库系统之间略有不同的系统视图：

- 本地的 server\_ &nbsp; - &nbsp; 前缀  
- 用于云中的 Azure SQL DB 服务的 database\_ &nbsp; - &nbsp; 前缀  

为便于说明，下表列出并比较了系统视图的两个子集。 为简洁起见，将子集限制为也包含字符串 `_event` 的视图名称。 这些子集具有不同的名称前缀，因为它们来自两个不同的数据库系统。

| 本地 2017 中的名称 | 云服务中的名称 |
| :------------------------- | :---------------------- |
| server_event_notifications<br />server_event_session_actions<br />server_event_session_events<br />server_event_session_fields<br />server_event_session_targets<br />server_event_sessions<br />server_events<br />server_trigger_events | database_event_session_actions<br />database_event_session_events<br />database_event_session_fields<br />database_event_session_targets<br />database_event_sessions |
| &nbsp; | &nbsp; |

上表中的两个列表精确到 2019 年 6 月。 但此处的表内容可能会过时，因为不会在此处保留其内容。 有关准确的列表，请运行以下 T-SQL SELECT 语句。 对每个数据库系统各运行一次 SELECT。

```sql
SELECT name
    FROM sys.all_objects
    WHERE
        (name LIKE 'database\_%' { ESCAPE '\' } OR
         name LIKE 'server\_%' { ESCAPE '\' })
        AND name LIKE '%\_event%' { ESCAPE '\' }
        AND type = 'V'
    ORDER BY name;
```

<!--
The creation of this docs/includes/ file was prompted by Issue 2211 (https://github.com/MicrosoftDocs/sql-docs/issues/2211).
Initial PR was PR 10427 (https://github.com/MicrosoftDocs/sql-docs-pr/pull/10427).
The complaint was that a specific T-SQL code block failed on Azure SQL Database.

GeneMi  ,  2019/05/28
-->
