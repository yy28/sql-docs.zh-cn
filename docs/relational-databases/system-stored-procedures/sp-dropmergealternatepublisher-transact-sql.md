---
title: sp_dropmergealternatepublisher （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergealternatepublisher
- sp_dropmergealternatepublisher_TSQL
helpviewer_keywords:
- sp_dropmergealternatepublisher
ms.assetid: a7dee4e2-2a60-41da-9d1d-6f991d7e2c5e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c8b80b4e5dd7caddb521ff8febffb0bd1baa36e7
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830089"
---
# <a name="sp_dropmergealternatepublisher-transact-sql"></a>sp_dropmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除合并发布中的备用发布服务器。 此存储过程在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropmergealaternatepublisher [ @publisher = ] 'publisher'    , [ @publisher_db = ] 'publisher_db'    , [ @publication = ] 'publication'    , [ @alternate_publisher = ] 'alternate_publisher'    , [ @alternate_publisher_db = ] 'alternate_publisher_db'    , [ @alternate_publication = ] 'alternate_publication'  
```  
  
## <a name="arguments"></a>参数  
`[ @publisher = ] 'publisher'`当前发布服务器的名称。 *发布服务器*的**sysname**，无默认值。  
  
`[ @publisher_db = ] 'publisher_db'`当前发布数据库的名称。 *publisher_db* **sysname**，无默认值。  
  
`[ @publication = ] 'publication'`当前发布的名称。 *发布*为**sysname**，无默认值。  
  
`[ @alternate_publisher = ] 'alternate_publisher'`要作为备用同步伙伴删除的备用发布服务器的名称。 *alternate_publisher* **sysname**，无默认值。  
  
`[ @alternate_publisher_db = ] 'alternate_publisher_db'`要作为备用同步伙伴发布数据库删除的发布数据库的名称。 *alternate_publisher_db* **sysname**，无默认值。  
  
`[ @alternate_publication = ] 'alternate_publication'`要作为备用同步伙伴发布删除的发布的名称。 *alternate_publication* **sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_dropmergealternatepublisher**用于合并复制。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_dropmergelternatepublisher**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_addmergealternatepublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergealternatepublisher-transact-sql.md)  
  
  
