---
description: DBCC dllname (FREE) (Transact-SQL)
title: DBCC dllname (FREE) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- dbcc_dllname_(FREE)_TSQL
- dllname
- dbcc dllname (FREE)
- FREE
- dbcc_dllname(FREE)_TSQL
- FREE_TSQL
- dllname_TSQL
- dbcc dllname(FREE)
dev_langs:
- TSQL
helpviewer_keywords:
- DLL unloading [SQL Server]
- DBCC dllname (FREE)
- freeing DLLs
- unloading DLLs
ms.assetid: 1eb71c17-fe15-430b-8916-e4e312dcf9c0
author: pmasl
ms.author: umajay
ms.openlocfilehash: 0fd6d497ed6738d6ef290645df9bcad18ca6df32
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116931"
---
# <a name="dbcc-dllname-free-transact-sql"></a>DBCC dllname (FREE) (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
从内存中上载指定的扩展存储过程 DLL。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
```syntaxsql
DBCC <dllname> ( FREE ) [ WITH NO_INFOMSGS ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>参数
 \<*dllname*>  
 要从内存中释放的 DLL 名称。  
  
 WITH NO_INFOMSGS  
 取消显示所有信息性消息。  
  
## <a name="remarks"></a>备注
执行扩展存储过程时，DLL 仍保持由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例加载，直到服务器关闭为止。 此语句允许从内存中卸载 DLL，而不用关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 若要显示目前由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 加载的 DLL 文件，请执行 sp_helpextendedproc
  
## <a name="result-sets"></a>结果集  
指定了有效的 DLL 之后，DBCC dllname (FREE) 将返回：
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>权限  
要求具有 **sysadmin** 固定服务器角色或 **db_owner** 固定数据库角色的成员身份。
  
## <a name="examples"></a>示例  
以下示例假设以 xp_sample.dll 实现 `xp_sample` 且已执行完毕。 DBCC \<*dllname*> (FREE) 卸载与 `xp_sample` 扩展过程相关联的 xp_sample.dll 文件。
  
```sql  
DBCC xp_sample (FREE);  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[扩展存储过程的执行特征](../../relational-databases/extended-stored-procedures-programming/execution-characteristics-of-extended-stored-procedures.md)  
[sp_addextendedproc (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)  
[sp_dropextendedproc (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
[sp_helpextendedproc (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)  
[卸载扩展存储过程 DLL](../../relational-databases/extended-stored-procedures-programming/unloading-an-extended-stored-procedure-dll.md)
  
  
