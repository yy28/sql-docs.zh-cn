---
title: 用于内存优化表上事务重试逻辑的指导原则 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f2a35c37-4449-49ee-8bba-928028f1de66
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 86c97342ff2a9e3ed3facb6612c0899c3b436edc
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393131"
---
# <a name="guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables"></a>内存优化表事务重试逻辑准则
  有一些与访问内存优化表的事务有关的错误情形。  
  
-   41302. 当前事务尝试更新自事务启动以来已更新过的记录。  
  
-   41305. 因某个可重复读取验证失败，当前事务无法提交。  
  
-   41325. 因某个序列化读取验证失败，当前事务无法提交。  
  
-   41301. 当前事务所依赖的前一事务已终止，当前事务无法再提交。  
  
 这些错误通常是由并发执行的事务相互干扰而产生的。 常见的纠正措施是重试事务。  
  
 有关这些错误情况的详细信息，请参阅部分上冲突检测、 验证和提交依赖关系检查中[内存优化表中的事务](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
 内存优化表不会产生死锁（错误代码为 1205）。 对于内存优化表不使用锁。 但是，如果应用程序已包含死锁重试逻辑，则可能会扩展现有逻辑，以包含新的错误代码。  
  
## <a name="considerations-for-retrying"></a>有关重试的注意事项  
 应用程序通常会遭遇事务相互冲突，而需要实现重试逻辑以解决这些冲突。 遭遇冲突的次数取决于若干因素：  
  
-   个别行争用。 随着事务尝试更新同一行的次数的增加，发生冲突的可能性也会增加。  
  
-   REPEATABLE READ 事务读取的行数。 读取的行数越多，这些行中的某些行被并发事务更新的几率就越大。 这将导致重复性读取验证失败。  
  
-   SERIALIZABLE 事务使用的扫描范围的大小。 扫描范围越大，并发事务引入虚拟行的几率就越大，从而导致序列化验证失败。  
  
     应用程序很难避免此类冲突，因而需要重试逻辑。  
  
> [!IMPORTANT]  
>  访问内存优化表的读/写事务需要重试逻辑。  
  
### <a name="considerations-for-read-only-transactions-and-natively-compiled-stored-procedures"></a>有关只读事务和本机编译存储过程的注意事项  
 延续本机编译存储过程单次执行的只读事务不需要 REPEATABLE READ 和 SERIALIZABLE 事务验证。 只读事务不会造成写入冲突。  
  
 但是，依赖关系失败仍可能发生。 依赖关系失败没有冲突造成的错误那样常见。 因此，在许多情况下，延续本机编译存储过程单次执行的只读事务不需要特定的重试逻辑。  
  
### <a name="considerations-for-read-only-transactions-and-cross-container-transactions"></a>有关只读事务和跨容器事务的注意事项  
 如果所有内存优化表都是在 SNAPSHOT 隔离的情况下访问的，则只读跨容器事务（即在本机编译存储过程上下文之外启动的事务）不执行验证。 但是，当在 REPEATABLE READ 或 SERIALIZABLE 隔离下访问内存优化表时，将在提交时间执行验证。 在这种情况下，可能需要重试逻辑。  
  
 详细信息，请参阅部分中的交叉容器事务[事务隔离级别](../../2014/database-engine/transaction-isolation-levels.md)。  
  
## <a name="implementing-retry-logic"></a>实现重试逻辑  
 就像访问内存优化表的所有事务一样，您需要考虑使用重试逻辑来处理可能出现的失败，例如写入冲突（错误代码 41302）或依赖关系错误（错误代码 41301）。 在大多数应用程序中，失败率很低，但仍有必要通过重试事务来处理失败。 建议通过两种方法实现重试逻辑：  
  
-   客户端重试。 客户端重试是一般情况下实现重试逻辑的首选方法。 客户端应用程序捕获事务抛出的错误，并重试该事务。 如果现有的客户端应用程序有处理死锁的重试逻辑，可以扩展该应用程序以处理新错误代码。  
  
-   使用包装存储过程。 客户端调用解释型 [!INCLUDE[tsql](../includes/tsql-md.md)] 存储过程，它将调用本机编译的存储过程或执行该事务。 然后，包装过程使用 try/catch 逻辑捕获错误并重试过程调用（如果需要）。 有可能结果已在失败前返回到客户端，所以客户端不会知道要放弃它们。 因此，为安全起见，最好在此方法中仅使用不向客户端返回任何结果集的本机编译的存储过程。  
  
 重试逻辑可在 [!INCLUDE[tsql](../includes/tsql-md.md)] 或中间层中的应用程序代码中实现。  
  
 考虑重试逻辑时的两个可能因素有：  
  
-   客户端应用程序具有针对其他错误代码的重试逻辑，如 1205，可以加以扩展。  
  
-   冲突不常见，而借助准备好的执行减少端到端延迟很重要。 有关详细信息执行本机编译存储的过程直接，请参阅[Natively Compiled Stored Procedures](../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)。  
  
 下面的示例演示解释型 [!INCLUDE[tsql](../includes/tsql-md.md)] 存储过程中的重试逻辑，它包含对本机编译存储过程或跨容器事务的调用。  
  
```tsql  
CREATE PROCEDURE usp_my_procedure @param1 type1, @param2 type2, ...  
AS  
BEGIN  
  -- number of retries – tune based on the workload  
  DECLARE @retry INT = 10  
  
  WHILE (@retry > 0)  
  BEGIN  
    BEGIN TRY  
  
      -- exec usp_my_native_proc @param1, @param2, ...  
  
      --       or  
  
      -- BEGIN TRANSACTION  
      --   …  
      -- COMMIT TRANSACTION  
  
      SET @retry = 0  
    END TRY  
    BEGIN CATCH  
      SET @retry -= 1  
  
      -- the error number for deadlocks (1205) does not need to be included for   
      -- transactions that do not access disk-based tables  
      IF (@retry > 0 AND error_number() in (41302, 41305, 41325, 41301, 1205))  
      BEGIN  
        -- these error conditions are transaction dooming - rollback the transaction  
        -- this is not needed if the transaction spans a single native proc execution  
        --   as the native proc will simply rollback when an error is thrown   
        IF XACT_STATE() = -1  
          ROLLBACK TRANSACTION  
  
        -- use a delay if there is a high rate of write conflicts (41302)  
        --   length of delay should depend on the typical duration of conflicting transactions  
        -- WAITFOR DELAY '00:00:00.001'  
      END  
      ELSE  
      BEGIN  
        -- insert custom error handling for other error conditions here  
  
        -- throw if this is not a qualifying error condition  
        ;THROW  
      END  
    END CATCH  
  END  
END  
```  
  
## <a name="see-also"></a>请参阅  
 [了解内存优化表上的事务](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [内存优化表中的事务](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [内存优化表事务隔离级别准则](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)  
  
  
