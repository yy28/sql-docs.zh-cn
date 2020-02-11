---
title: 创建本机编译的存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9525ef65973baa38ae19ba4681e4a93f949c004a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63071802"
---
# <a name="creating-natively-compiled-stored-procedures"></a>创建本机编译的存储过程
  本机编译的存储过程未实现完整 [!INCLUDE[tsql](../../includes/tsql-md.md)] 可编程性和查询外围应用。 某些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 构造不能在本机编译的存储过程内使用。 有关详细信息，请参阅[本机编译的存储过程中支持的构造](../in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)。  
  
 但是，有几个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能，仅本机编译的存储过程支持这些功能：  
  
-   原子块。 有关详细信息，请参阅 [Atomic Blocks](atomic-blocks-in-native-procedures.md)。  
  
-   本机编译存储过程中参数和变量上的 `NOT NULL` 约束。 不能将 `NULL` 值分配给声明为 `NOT NULL` 的参数或变量。 有关详细信息，请参阅 [DECLARE @local_variable (Transact-SQL)](/sql/t-sql/language-elements/declare-local-variable-transact-sql)。  
  
-   本机编译存储过程的架构绑定。  
  
 使用 [CREATE PROCEDURE (Transact-SQL)](/sql/t-sql/statements/create-procedure-transact-sql) 创建本机编译的存储过程。 下面的示例显示内存优化表以及用于将行插入表的本机编译存储过程。  
  
```sql  
create table dbo.Ord  
(OrdNo integer not null primary key nonclustered,   
 OrdDate datetime not null,   
 CustCode nvarchar(5) not null)   
 with (memory_optimized=on)  
go  
  
create procedure dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
with native_compilation, schemabinding, execute as owner  
as   
begin atomic with  
(transaction isolation level = snapshot,  
language = N'English')  
  
  declare @OrdDate datetime = getdate();  
  insert into dbo.Ord (OrdNo, CustCode, OrdDate) values (@OrdNo, @CustCode, @OrdDate);  
end  
go  
```  
  
 在代码示例中，`NATIVE_COMPILATION` 指示此 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程是本机编译的存储过程。 以下选项是必需的：  
  
|选项|说明|  
|------------|-----------------|  
|`SCHEMABINDING`|本机编译存储过程必须绑定到其引用的对象的架构。 这意味着不能删除该过程引用的表。 在该过程中引用的表必须包括其架构名称，并且\*在查询中不允许使用通配符（）。 此版本的 `SCHEMABINDING` 中的本机编译存储过程仅支持 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。|  
|`EXECUTE AS`|本机编译的存储过程不支持 `EXECUTE AS CALLER`，这是默认执行上下文。 因此，需要指定执行上下文。 支持选项`EXECUTE AS OWNER`、 `EXECUTE AS`*用户*和`EXECUTE AS SELF` 。|  
|`BEGIN ATOMIC`|本机编译的存储过程正文必须由恰好一个原子块构成。 原子块确保存储过程的原子执行。 如果在活动事务的上下文外调用该过程，它将开始一个新事务，这个新事务在原子块的末尾提交。 本机编译存储过程中的原子块具有两个必需的选项：<br /><br /> `TRANSACTION ISOLATION LEVEL`. 请参阅支持的隔离级别的[事务隔离级别](../../database-engine/transaction-isolation-levels.md)。<br /><br /> `LANGUAGE`. 存储过程的语言必须设置为可用语言或语言别名之一。|  
  
 通过 `EXECUTE AS` 进行模拟可能会导致 `EXECUTE AS` 和 Windows 登录名出错。 如果用户帐户使用 Windows 身份验证，则用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的服务帐户与 Windows 登录名所在的域之间必须存在完全信任。 如果没有完全信任，则在创建本机编译的存储过程时返回以下错误消息：消息15404、无法获取有关 Windows NT 组/用户 "username" 的信息，错误代码0x5。  
  
 若要解决此错误，请使用以下选项之一：  
  
-   使用与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务的 Windows 用户处于相同域中的帐户。  
  
-   如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 正在使用 Network Service 或 Local System 等计算机帐户，则包含 Windows 用户的域必须信任该计算机。  
  
-   使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证。  
  
 在创建本机编译的存储过程时还可能会看到错误 15517。 有关详细信息，请参阅[MSSQLSERVER_15517](../errors-events/mssqlserver-15517-database-engine-error.md)。  
  
## <a name="updating-a-natively-compiled-stored-procedure"></a>更新本机编译的存储过程  
 不支持对本机编译的存储过程执行更改操作。 修改本机编译的存储过程的一种方法是删除再重新创建该存储过程：  
  
1.  生成对该存储过程的权限的脚本。  
  
2.  生成该存储过程的脚本并另存为备份（可选）。  
  
3.  删除该存储过程。  
  
4.  创建更改后的存储过程。  
  
5.  将脚本化的权限重新应用到该存储过程。  
  
 此方法的缺点是从步骤 3 开始到步骤 5 结束应用程序将会脱机。 这可能需要几秒钟时间，并且使用应用程序的客户端可能看到错误消息。  
  
 另一种高效修改本机编译的存储过程的方法是首先创建存储过程的新版本。 此处，本机编译的存储过程具有一个关联的版本号。 我们将旧版本称为 SP_Vold，将新版本称为 SP_Vnew。  
  
1.  为 SP_Vold 上的权限生成脚本。  
  
2.  创建 SP_Vnew。  
  
3.  将 SP_Vold 的权限应用到 SP_Vnew。  
  
4.  更新对 SP_Vold 的引用以指向 SP_Vnew。 这可以通过不同方式实现，例如：  
  
     使用一个包装（基于磁盘的）存储过程，并修改该过程以指向 SP_Vnew。 此方法的缺点是间接影响性能。  
  
    ```sql  
    ALTER PROCEDURE dbo.SP p1,...,pn  
    AS  
      EXEC dbo.SP_Vnew p1,...,pn  
    GO  
    ```  
  
5.  删除 SP_Vold（可选）。  
  
 此方法的优势在于应用程序不会脱机。 但是，需要做更多的工作来维护引用并确保它们始终指向存储过程的最新版本。  
  
## <a name="see-also"></a>另请参阅  
 [本机编译的存储过程](natively-compiled-stored-procedures.md)  
  
  
