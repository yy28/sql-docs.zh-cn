---
title: "catalog.start_execution （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f8663ff3-aa98-4dd8-b850-b21efada0b87
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 8edb51596198f27f00c1b78ddc8b3075ad035143
ms.contentlocale: zh-cn
ms.lasthandoff: 10/20/2017

---
# <a name="catalogstartexecution-ssisdb-database"></a>catalog.start_execution（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中启动执行实例。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.start_execution [@execution_id =] execution_id [, [@retry_count =] retry_count]  
```  
  
## <a name="arguments"></a>参数  
 [@execution_id =] *execution_id*  
 执行实例的唯一标识符。 *Execution_id*是**bigint**。
 
 [@retry_count =] *retry_count*  
 如果执行失败重试计数。 仅当执行在横向扩展设置将生效。此参数可选。 如果未指定，则会将其值设置为 0。 *Retry_count*是**int**。
  
## <a name="remarks"></a>注释  
 执行用于指定包在包执行的单个实例期间使用的参数值。 在创建执行实例后，但在启动此实例之前，可能重新部署对应的项目。 在这种情况下，执行实例引用的项目已过时。 此无效的引用将导致失败的存储的过程。  
  
> [!NOTE]  
>  只能启动执行一次。 若要启动的执行实例，它必须在创建的状态 (值为`1`中**状态**列[catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md)视图)。  
  
## <a name="example"></a>示例  
 以下示例调用 catalog.create_execution 来创建 Child1.dtsx 包的执行实例。 Integration Services Project1 包含该包。 该示例调用 catalog.set_execution_parameter_value 来设置 Parameter1、Parameter2 和 LOGGING_LEVEL 参数的值。 该示例调用 catalog.start_execution 启动一个执行实例。  
  
```sql
Declare @execution_id bigint  
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Child1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'TestDeply4', @project_name=N'Integration Services Project1', @use32bitruntime=False, @reference_id=Null  
Select @execution_id  
DECLARE @var0 sql_variant = N'Child1.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter1', @parameter_value=@var0  
DECLARE @var1 sql_variant = N'Child2.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter2', @parameter_value=@var1  
DECLARE @var2 smallint = 1  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var2  
EXEC [SSISDB].[catalog].[start_execution] @execution_id  
GO  
```  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对执行实例的 READ 和 MODIFY 权限，针对项目的 READ 和 EXECUTE 权限，针对引用环境的 READ 权限（如果适用）  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   用户没有适当的权限  
  
-   执行标识符无效  
  
-   执行已被启动或已完成；只能启动执行一次  
  
-   与项目关联的环境引用无效  
  
-   尚未设置所需的参数值  
  
-   与实例执行关联的项目版本已过时；只可执行项目的最新版本  
  
  

