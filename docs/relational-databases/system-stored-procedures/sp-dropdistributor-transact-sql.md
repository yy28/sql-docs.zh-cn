---
title: sp_dropdistributor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropdistributor
- sp_dropdistributor_TSQL
helpviewer_keywords:
- sp_dropdistributor
ms.assetid: 0644032f-5ff0-4718-8dde-321bc9967a03
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e321b5e5976192146f9cd8d993304d5f5ae55e67
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43029057"
---
# <a name="spdropdistributor-transact-sql"></a>sp_dropdistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  卸载分发服务器。 此存储过程在分发服务器上除分发数据库之外的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropdistributor [ [ @no_checks= ] no_checks ]   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@no_checks=**] *no_checks*  
 指示在删除分发服务器之前是否检查有无依赖对象。 *no_checks*是**位**，默认值为 0。  
  
 如果**0**， **sp_dropdistributor**检查以确保除分发服务器上的所有发布和分发对象已被都删除。  
  
 如果**1**， **sp_dropdistributor**删除然后再卸载分发服务器上的所有发布和分发对象。  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 指示是否在未连接到分发服务器的情况下执行此存储过程。 *ignore_distributor*是**位**，默认值为**0**。  
  
 如果**0**， **sp_dropdistributor**连接到分发服务器，并删除所有复制对象。 如果**sp_dropdistributor**无法连接到分发服务器，则存储的过程将失败。  
  
 如果**1**、 没有连接到分发服务器并不会删除复制对象。 如果分发服务器正在卸载或持久脱机，才使用它。 直到分发服务器在未来某个时间重新安装之后，才会删除分发服务器中的该发布服务器的对象。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_dropdistributor**用于所有类型的复制。  
  
 如果在服务器上，存在其他发布服务器或分发对象**sp_dropdistributor**会失败，除非**@no_checks**设置为**1**。  
  
 必须通过执行删除分发数据库之后执行此存储的过程**sp_dropdistributiondb**。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributor-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_dropdistributor**。  
  
## <a name="see-also"></a>请参阅  
 [禁用发布和分发](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistributor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [sp_changedistributor_property &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_helpdistributor (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
