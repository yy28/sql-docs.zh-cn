---
title: "catalog.create_execution （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 45d0c2f6-1f38-445f-ac06-e2a01f6ac600
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 7e9d38935a91bba81359bee7fdbd64dba86d0d26
ms.contentlocale: zh-cn
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreateexecution-ssisdb-database"></a>catalog.create_execution（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中创建执行实例。  
  
 此存储过程使用默认服务器日志记录级别。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.create_execution [@folder_name = folder_name  
     , [@project_name =] project_name  
     , [@package_name =] package_name  
  [  , [@reference_id =] reference_id ]  
  [  , [@use32bitruntime =] use32bitruntime ] 
  [  , [@runinscaleout =] runinscaleout ]
  [  , [@useanyworker =] useanyworker ] 
     , [@execution_id =] execution_id OUTPUT  
```  
  
## <a name="arguments"></a>参数  
 [@folder_name =] *folder_name*  
 包含要执行的包的文件夹名称。 *Folder_name*是**nvarchar （128)**。  
  
 [@project_name =]*文件的内容*  
 包含要执行的包的项目的名称。 *文件的内容*是**nvarchar （128)**。  
  
 [@package_name =]*包名称*  
 包含要执行的包的名称。 *Package_name*是**nvarchar(260)**。  
  
 [@reference_id =] *reference_id*  
 环境引用的唯一标识符。 此参数可选。 *Reference_id*是**bigint**。  
  
 [@use32bitruntime =] *use32bitruntime*  
 指示是否应使用 32 位运行时在 64 位操作系统上运行包。 使用值为 1 来执行与 32 位运行时包，在 64 位操作系统上运行时。 使用值 0 表示在 64 位操作系统上运行时，使用 64 位运行时执行此包。 此参数可选。 *Use32bitruntime*是**位**。  
 
 [@runinscaleout =] *runinscaleout*  
 指示是否正在执行向外扩展。使用值为 1 来向外扩展在执行包。使用值为 0 来执行软件包，无需向外扩展。此参数可选。 如果未指定，则会将其值设置为 DEFAULT_EXECUTION_MODE [SSISDB] 中。[目录]。[catalog_properties]。 *Runinscaleout*是**位**。 
 
 [@useanyworker =] *useanyworker*  
  指示是否允许辅助出任何规模进行执行。 使用值为 1 来执行辅助出任何规模的包。 使用值 0 指示不所有横向扩展辅助进程都才能执行包。 此参数可选。 如果未指定，则将其值设置为 1。 *Useanyworker*是**位**。 
  
 [@execution_id =] *execution_id*  
 返回执行实例的唯一标识符。 *Execution_id*是**bigint**。  

  
## <a name="remarks"></a>注释  
 使用执行来指定参数值，包在单个包执行实例中将使用这些参数值。  
  
 如果使用指定的环境引用*reference_id*参数，该存储过程填充文本值或从相应的环境变量中引用的值作为项目和包参数。 如果指定了环境引用，则在包执行过程中将使用默认参数值。 若要确定完全将哪些值用于执行的特定实例，请使用*execution_id*输出参数值从此存储的过程和查询[execution_parameter_values](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)视图。  
  
 在执行中只能指定标记为入口点包的包。 如果指定的包不是入口点，则执行失败。  
  
## <a name="example"></a>示例  
 下面的示例调用 catalog.create_execution 创建了不在向外扩展的 Child1.dtsx 包执行的实例。Integration Services Project1 包含该包。 该示例调用 catalog.set_execution_parameter_value 来设置 Parameter1、Parameter2 和 LOGGING_LEVEL 参数的值。 该示例调用 catalog.start_execution 启动一个执行实例。  
  
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
  
-   针对项目的 READ 和 EXECUTE 权限，如果适用，则需要针对引用环境的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  

 如果@runinscaleout为 1，存储的过程需要以下权限之一：
 
-   成员资格**ssis_admin**数据库角色

-   成员资格**ssis_cluster_executor**数据库角色

-   成员资格**sysadmin**服务器角色
  
## <a name="errors-and-warnings"></a>错误和警告  
 以下列表描述某些可能会发出错误或警告的情况：  
  
-   该包不存在。  
  
-   用户不具备适当的权限。  
  
-   环境引用， *reference_id*，而无效。  
  
-   指定的包不是入口点包。  
  
-   引用环境变量的数据类型不同于项目或包参数的数据类型。  
  
-   项目或包包含需要值的参数，但尚未分配任何值。  
  
-   环境引用，该环境中找不到引用的环境变量*reference_id*，指定。  
  
## <a name="see-also"></a>另请参阅  
 [catalog.start_execution &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   
 [catalog.set_execution_parameter_value（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [catalog.add_execution_worker &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)  
  

