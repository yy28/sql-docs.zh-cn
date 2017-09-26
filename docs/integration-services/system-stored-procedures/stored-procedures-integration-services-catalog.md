---
title: "存储过程 （Integration Services 目录） |Microsoft 文档"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- stored procedures [Integration Services]
ms.assetid: a6ccd884-108f-4fb6-95ad-00b9cb65d5d6
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 21715bf65f3a85669dfe823511ddb9b6c2dd4d57
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="stored-procedures-integration-services-catalog"></a>存储过程（Integration Services 目录）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本节介绍可用于管理已部署到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 实例的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程。  
  
 调用[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]存储过程来添加、 删除、 修改或执行存储在对象**SSISDB**目录。  
  
 该目录的默认名称是 SSISDB。 目录中存储的对象包括项目、包、参数环境和操作历史记录。  
  
 您可以直接使用数据库视图和存储过程，或者编写调用托管 API 的自定义代码。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 和托管 API 查询这些视图，并调用本节中介绍的存储过程来执行许多任务。  
  
## <a name="in-this-section"></a>本节内容  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
 在包数据流中添加组件输出的数据分流点。  
  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
 将数据分流点添加到包数据流中特定的数据流路径。  
  
 [catalog.check_schema_version](../../integration-services/system-stored-procedures/catalog-check-schema-version.md)  
 确定 SSISDB 目录架构与 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 二进制文件（ISServerExec 和 SQLCLR 程序集）是否兼容。  
  
 [catalog.clear_object_parameter_value &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md)  
 清除存储在服务器上的现有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目或包的参数的值。  
  
 [catalog.configure_catalog &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)  
 通过将目录属性设置为指定的值，配置 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录。  
  
 [catalog.create_environment（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中创建环境。  
  
 [catalog.create_environment_reference（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中为项目创建环境引用。  
  
 [catalog.create_environment_variable（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中创建环境变量。  
  
 [catalog.create_execution &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中创建执行实例。  
  
 [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
 导致暂停正在运行的包并创建转储文件。  
  
 [catalog.create_folder（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中创建一个文件夹。  
  
 [catalog.delete_environment（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
 从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的某个文件夹删除环境。  
  
 [catalog.delete_environment_reference（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
 从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录的项目中删除一个环境引用。  
  
 [catalog.delete_environment_variable（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
 从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的某个环境删除环境变量。  
  
 [catalog.delete_folder（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
 从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录删除文件夹。  
  
 [catalog.delete_project（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
 从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的某个文件夹删除现有项目。  
  
 [catalog.deny_permission &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md)  
 拒绝对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的某个安全对象的权限。  
  
 [catalog.deploy_project（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
 将项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的文件夹，或更新以前部署的现有项目。  
  
 [catalog.get_parameter_values &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md)  
 从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的项目和对应包中解析和检索默认参数值。  
  
 [catalog.get_project（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
 检索 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中现有项目的属性。  
  
 [catalog.grant_permission &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)  
 授予对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的某个安全对象的权限。  
  
 [catalog.move_environment（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
 将环境从一个文件夹移到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的另一个文件夹。  
  
 [catalog.move_project（SSISDB 数据库）](../Topic/catalog.move_project%20\(\(SSISDB%20Database\).md)  
 将项目从一个文件夹移到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的另一个文件夹。  
  
 [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md)  
 从执行中的组件输出删除数据分流点。  
  
 [catalog.rename_environment（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中重命名环境。  
  
 [catalog.rename_folder（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中重命名一个文件夹。  
  
 [catalog.restore_project（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
 将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的项目还原到以前的版本。  
  
 [catalog.revoke_permission &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中撤消对某个安全对象的权限。  
  
 [catalog.set_environment_property（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中设置环境的属性。  
  
 [catalog.set_environment_reference_type（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
 设置与 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中某个项目的现有环境引用关联的引用类型和环境名称。  
  
 [catalog.set_environment_variable_property（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中设置环境变量的属性。  
  
 [catalog.set_environment_variable_protection &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中设置环境变量的敏感性位。  
  
 [catalog.set_environment_variable_value（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中设置环境变量的值。  
  
 [catalog.set_execution_parameter_value（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的执行实例设置参数的值。  
  
 [catalog.set_execution_property_override_value](../../integration-services/system-stored-procedures/catalog-set-execution-property-override-value.md)  
 为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的执行实例设置属性的值。  
  
 [catalog.set_folder_description（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中设置文件夹的说明。  
  
 [catalog.set_object_parameter_value &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中设置参数的值。 将值与环境变量关联，或者如果未指定任何其他值，则分配默认情况下使用的文本值。  
  
 [catalog.start_execution &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中启动执行实例。  
  
 [catalog.startup](../../integration-services/system-stored-procedures/catalog-startup.md)  
 对 SSISDB 目录的操作状态进行维护。  
  
 [catalog.stop_operation &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中停止执行的验证或实例。  
  
 [catalog.validate_package &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md)  
 以异步方式验证 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的包。  
  
 [catalog.validate_project &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md)  
 以异步方式验证 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的项目。  
  
[catalog.add_execution_worker &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)   
将添加[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]缩放出辅助到向外扩展中执行的实例。

[catalog.enable_worker_agent &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)   
为与此工作 Master 出缩放启用横向扩展辅助进程[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]目录。

[catalog.disable_worker_agent &#40;SSISDB 数据库 &#41;](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)   
禁用与此工作 Master 出缩放的横向扩展辅助进程[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]目录。



