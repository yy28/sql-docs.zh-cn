---
title: "catalog.cleanup_server_log |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0dedb685-d3a6-4bd6-8afd-58d98853deee
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1195bbfcc77cb6b96ea5a68cd1a95c2b2126a81e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcleanupserverlog"></a>catalog.cleanup_server_log
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  清除操作日志，使 SSISDB 数据库进入可让您更改 SERVER_OPERATION_ENCRYPTION_LEVEL 属性的值的状态。  
  
## <a name="syntax"></a>语法  
  
```sql
catalog.cleanup_server_log  
```  
  
## <a name="arguments"></a>参数  
 无。  
  
## <a name="return-code-values"></a>返回代码值  
 针对成功和失败的 1 为 0。  
  
## <a name="result-sets"></a>结果集  
 无。  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   读取和执行项目的权限，如果适用，在引用的环境上的读取权限。  
  
-   中的成员身份**ssis_admin**数据库角色。  
  
-   成员资格**sysadmin**服务器角色。  
  
## <a name="errors-and-warnings"></a>错误和警告  
 此存储的过程可引发以下方案中的错误：  
  
-   有一些 SSISDB 数据库中的一个或多个活动操作。  
  
-   SSISDB 数据库不处于单用户模式。  
  
## <a name="remarks"></a>注释  
 SQL Server 2012 Service Pack 2 添加到 SERVER_OPERATION_ENCRYPTION_LEVEL 属性**internal.catalog_properties**表。 此属性具有两个可能值：  
  
-   **PER_EXECUTION (1)** – 的证书和对称密钥用于保护敏感执行参数，每次执行创建执行日志。 这是默认值。 你可能会遇到性能问题 （死锁，失败的维护作业等） 在生产环境中由于每次执行生成的证书/密钥。 但是，此设置可以提供比其他值 (2) 更高级别的安全性。  
  
-   **PER_PROJECT (2)** – 每个项目创建的证书和对称密钥用于保护敏感参数。 这可让你更好的性能比 PER_EXECUTION 级别因为生成的密钥和证书是一次为一个项目而不是每次执行。  
  
 你必须运行[catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md)之前从 1 到 2 从 1 到 2 （或），可以更改 SERVER_OPERATION_ENCRYPTION_LEVEL 存储过程。 运行此存储过程之前，请执行以下操作：  
  
1.  确保属性 OPERATION_CLEANUP_ENABLED 的值设置为 TRUE [catalog.catalog_properties &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)表。  
  
2.  设置为单用户模式的 Integration Services 数据库 (SSISDB)。 在 SQL Server Management Studio，启动 SSISDB 数据库属性对话框中，切换到选项选项卡，并将限制访问属性设置为单用户模式 (SINGLE_USER)。 运行 cleanup_server_log 后存储的过程，将属性值设置回原始值。  
  
3.  运行存储的过程[catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md)。  
  
4.  现在，请继续并更改中的 SERVER_OPERATION_ENCRYPTION_LEVEL 属性的值[catalog.catalog_properties &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)表。  
  
5.  运行存储的过程[catalog.cleanup_server_execution_keys](../../integration-services/system-stored-procedures/catalog-cleanup-server-execution-keys.md)清理 SSISDB 数据库中的证书密钥。 从 SSISDB 数据库中删除证书和密钥可能需要很长时间，以便它应定期在非高峰时间运行。  
  
     你可以指定的作用域或级别 （执行与项目） 和要删除的键数。 删除的默认批处理大小为 1000年。 当你将级别设置为 2 时，则会删除密钥和证书仅当关联的项目已被删除。  
  
 有关详细信息，请参阅以下知识库文章。 [修复： 在 SQL Server 2012 中存储的 SSISDB 用作你的部署时的性能问题](http://support.microsoft.com/kb/2972285)  
  
## <a name="example"></a>示例  
 下面的示例调用 cleanup_server_log 存储过程。  
  
```sql  
USE [SSISDB]  
GO  
  
DECLARE@return_value int  
EXEC@return_value = [internal].[cleanup_server_log]  
SELECT'Return Value' = @return_value  
GO   
```  
  
  
