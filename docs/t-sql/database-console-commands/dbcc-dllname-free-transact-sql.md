---
title: "DBCC dll 名称 （免费） (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e6d70bdab3515c883ea6f541ece6857f8ecda914
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-dllname-free-transact-sql"></a>DBCC dllname (FREE) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]卸载指定扩展存储的过程 DLL 从内存。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
```sql
DBCC <dllname> ( FREE ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
 \<*dll 名称*>  
 要从内存中释放的 DLL 名称。  
  
 WITH NO_INFOMSGS  
 取消显示所有信息性消息。  
  
## <a name="remarks"></a>注释
执行扩展存储过程时，DLL 仍保持由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例加载，直到服务器关闭为止。 此语句允许从内存中卸载 DLL，而不用关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 若要显示当前加载的 DLL 文件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，执行**sp_helpextendedproc**
  
## <a name="result-sets"></a>结果集  
指定有效的 DLL 时，DBCC *dll 名称*（免费） 返回：
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
要求具有 **sysadmin** 固定服务器角色或 **db_owner** 固定数据库角色的成员身份。
  
## <a name="examples"></a>示例  
下面的示例假定`xp_sample`作为 xp_sample.dll 实现，并已执行。 DBCC \< *dll 名称*> 与相关联 xp_sample.dll 文件 （免费） 卸载`xp_sample`扩展过程。
  
```sql  
DBCC xp_sample (FREE);  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[扩展存储过程的执行特征](../../relational-databases/extended-stored-procedures-programming/execution-characteristics-of-extended-stored-procedures.md)  
[sp_addextendedproc &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)  
[sp_dropextendedproc &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
[sp_helpextendedproc &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)  
[卸载扩展存储过程 DLL](../../relational-databases/extended-stored-procedures-programming/unloading-an-extended-stored-procedure-dll.md)
  
  

