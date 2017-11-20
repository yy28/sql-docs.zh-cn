---
title: "禁用 Stretch Database 并恢复远程数据 | Microsoft Docs"
ms.custom: 
ms.date: 08/05/2016
ms.prod: stretch-database
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, disabling
- disabling Stretch Database
ms.assetid: c1bbb24e-47e3-46aa-b786-fcadf9fb65ce
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: dc5f97519cc9c2916f164b4905e164a273ef2d58
ms.contentlocale: zh-cn
ms.lasthandoff: 07/29/2017

---
# <a name="disable-stretch-database-and-bring-back-remote-data"></a>禁用 Stretch Database 并恢复远程数据
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  若要禁用表的 Stretch Database，请在 SQL Server Management Studio 中为表选择“拉伸”  。 然后选择以下选项之一：  
  
-   **禁用 | 从 Azure 返回数据**。 将表中的远程数据从 Azure 复制回 SQL Server，然后禁用该表的 Stretch Database。 此操作会产生数据传输成本，并且不能取消。  
  
-   **禁用 | 将数据保留在 Azure 中**。 禁用表的 Stretch Database。  放弃 Azure 中的表的远程数据。  
  
 还可以使用 Transact-SQL 禁用表或数据库的 Stretch Database。  
  
 禁用表的 Stretch Database 之后，将停止数据迁移，查询结果不再包括远程表中的结果。  
  
 如果只想暂停数据迁移，请参阅 [暂停和恢复数据迁移 (Stretch Database)](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)。  
  
> [!NOTE]
> 禁用表或数据库的 Stretch Database 不会删除远程对象。 如果希望删除远程表或远程数据库，则需要使用 Azure 管理门户进行删除。 远程对象会继续产生 Azure 成本，直到删除它们。 有关详细信息，请参阅 [SQL Server Stretch Database 定价](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)。  
  
## <a name="disable-stretch-database-for-a-table"></a>禁用表的 Stretch Database  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-table"></a>使用 SQL Server Management Studio 禁用表的 Stretch Database  
  
1.  在 SQL Server Management Studio 的对象资源管理器中，选择希望对其禁用 Stretch Database 的表。  
  
2.  右键单击并选择“拉伸”，然后选择下列选项之一。  
  
    -   **禁用 | 从 Azure 返回数据**。 将表中的远程数据从 Azure 复制回 SQL Server，然后禁用该表的 Stretch Database。 此命令不能取消。  
  
        > [!NOTE]
        > 将表中的远程数据从 Azure 复制回 SQL Server 会产生数据传输成本。 有关详细信息，请参阅 [数据传输定价详细信息](https://azure.microsoft.com/pricing/details/data-transfers/)。  
  
         当所有远程数据已从 Azure 复制回 SQL Server 后，禁用表的“拉伸”。  
  
    -   **禁用 | 将数据保留在 Azure 中**。 禁用表的 Stretch Database。  放弃 Azure 中的表的远程数据。  
  
    > [!NOTE]
    > 禁用表的 Stretch Database 不会删除远程数据或远程表。 如要删除远程表，必须使用 Azure 管理门户进行删除。 远程表会继续产生 Azure 成本，直到被删除。 有关详细信息，请参阅 [SQL Server Stretch Database 定价](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)。  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-table"></a>使用 Transact-SQL 禁用表的 Stretch Database  
  
-   要禁用表的“延伸”和将表中的远程数据从 Azure 复制回 SQL Server，请运行以下命令。当所有远程数据已从 Azure 复制回 SQL Server 后，禁用表的“延伸”。

    此命令不能取消。  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ; 
    GO 
    ```  
  
    > [!NOTE]
    > 将表中的远程数据从 Azure 复制回 SQL Server 会产生数据传输成本。 有关详细信息，请参阅 [数据传输定价详细信息](https://azure.microsoft.com/pricing/details/data-transfers/)。    
  
-   要禁用表的“拉伸”并放弃远程数据，请运行以下命令。  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ; 
    GO
    ```  
  
> [!NOTE]
> 禁用表的 Stretch Database 不会删除远程数据或远程表。 如要删除远程表，必须使用 Azure 管理门户进行删除。 远程表会继续产生 Azure 成本，直到被删除。 有关详细信息，请参阅 [SQL Server Stretch Database 定价](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)。  
  
## <a name="disable-stretch-database-for-a-database"></a>禁用数据库的 Stretch Database  
 禁用数据库的 Stretch Database 之前，必须在数据库中已启用“拉伸”的各个表上禁用 Stretch Database。  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-database"></a>使用 SQL Server Management Studio 禁用数据库的 Stretch Database  
  
1.  在 SQL Server Management Studio 的对象资源管理器中，选择要对其禁用 Stretch Database 的数据库。  
  
2.  右键单击并选择“任务”，选择“延伸”，然后选择“禁用”。  
  
> [!NOTE]
> 禁用数据库的 Stretch Database 不会删除远程数据库。 如要删除远程表，必须使用 Azure 管理门户进行删除。 远程数据库会继续产生 Azure 成本，直到被删除。 有关详细信息，请参阅 [SQL Server Stretch Database 定价](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)。  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-database"></a>使用 Transact-SQL 禁用数据库的 Stretch Database  
 运行以下命令。  
  
```sql  
ALTER DATABASE <Stretch-enabled database name>  
    SET REMOTE_DATA_ARCHIVE = OFF ;  
GO 
```  
  
> [!NOTE]
> 禁用数据库的 Stretch Database 不会删除远程数据库。 如要删除远程表，必须使用 Azure 管理门户进行删除。 远程数据库会继续产生 Azure 成本，直到被删除。 有关详细信息，请参阅 [SQL Server Stretch Database 定价](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [暂停和恢复数据迁移 (Stretch Database)](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
  

