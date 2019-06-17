---
title: Integration Services (SSIS) 参数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cfd6a65e1561f252574ff919c8b63b0bbd57876f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892238"
---
# <a name="integration-services-ssis-parameters"></a>Integration Services (SSIS) 参数
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) 参数可用于在包执行时向包内的属性赋值。  您可以在项目级别创建“项目参数”  ，在包级别创建“包参数”。 项目参数可用于向项目中的一个或多个包提供项目接收的任何外部输入。 利用包参数，您不必编辑和重新部署包就可以修改包执行。  
  
 在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，您使用 **Project.params** 窗口创建、修改或删除项目参数。 通过使用 **设计器中的** “参数” [!INCLUDE[ssIS](../includes/ssis-md.md)] 选项卡来创建、修改和删除包参数。 通过使用 **“参数化”** 对话框，您可以将新的或现有的参数与任务属性相关联。 有关使用 **Project.params** 窗口和 **“参数”** 选项卡的详细信息，请参阅 [Create Parameters](create-parameters.md)。 有关 **“参数化”** 对话框的详细信息，请参阅 [Parameterize Dialog Box](parameterize-dialog-box.md)。  
  
## <a name="parameters-and-package-deployment-model"></a>参数和包部署模型  
 如果您正在使用包部署模型部署包，通常应使用配置而非参数。  
  
 使用包部署模型部署包含参数的包然后执行包时，在执行期间不调用参数。 如果包中包含包参数和表达式，则在运行时应用生成的值。 如果包中包含项目参数，则包执行可能会失败。  
  
## <a name="parameters-and-project-deployment-model"></a>参数和项目部署模型  
 将项目部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器时，您使用视图、存储过程和 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] UI 来管理项目和包参数。 有关详细信息，请参阅以下主题。  
  
-   [视图（Integration Services 目录）](/sql/integration-services/system-views/views-integration-services-catalog)  
  
-   [存储过程（Integration Services 目录）](/sql/integration-services/system-stored-procedures/stored-procedures-integration-services-catalog)  
  
-   [“配置”对话框](catalog/configure-dialog-box.md)  
  
-   [“执行包”对话框](../../2014/integration-services/execute-package-dialog-box.md)  
  
### <a name="parameter-values"></a>参数值  
 可以为参数最多赋予三个不同类型的值。 当启动包执行时，将单个值用于参数，然后将参数解析为最终的文字值。  
  
 下表列出了值的类型。  
  
|值名称|Description|值的类型|  
|----------------|-----------------|-------------------|  
|执行值|针对包执行的特定实例赋予的值。 此赋值将覆盖所有其他值，但仅应用于包执行的单个实例。|文字|  
|服务器值|在将项目部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器后在项目范围内赋予参数的值。 此值将覆盖设计默认值。|文字或环境变量引用|  
|设计值|在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中创建或编辑项目时赋予参数的值。 该值对于项目而言是持久的。|文字|  
  
 可以使用单个参数向多个包属性分配值。 只能从单个参数为单个包属性分配值。  
  
###  <a name="executions"></a> 执行和参数值  
  “执行”是表示包执行的单个实例的对象。 当您创建执行时，指定运行包所需的所有详细信息（如执行参数值）。 您还可以修改现有执行的参数值。  
  
 显式设置一个执行参数值时，该值仅适用于执行的特定实例。 使用执行值而非服务器值或设计值。 如果未显式设置执行值并指定了服务器值，则使用服务器值。  
  
 某一参数标记为必需时，必须为该参数指定服务器值或执行值。 否则，不会执行相应的包。 尽管该参数在设计时具有默认值，但在部署项目后，将永远不会再使用该默认值。  
  
#### <a name="environment-variables"></a>环境变量  
 如果某个参数引用某一环境变量，则来自该变量的文字值通过指定的环境引用进行解析并且应用于该参数。 用于包执行的最终的文字参数值称作执行参数值。 使用 **“执行”** 对话框来指定执行的环境引用  
  
 如果项目参数引用某一环境变量且无法在执行时解析来自该变量的文字值，则使用设计值。 不使用服务器值。  
  
 要查看分配给参数值的环境变量，请查询 catalog.object_parameters 视图。 有关详细信息，请参阅 [catalog.object_parameters（SSISDB 数据库）](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database)。  
  
#### <a name="determining-execution-parameter-values"></a>确定执行参数值  
 下面的 Transact-SQL 视图和存储过程可用于显示和设置参数值。  
  
 [catalog.execution_parameter_values（SSISDB 数据库）](/sql/integration-services/system-views/catalog-execution-parameter-values-ssisdb-database)（视图）  
 显示特定执行将使用的实际参数值  
  
 [catalog.get_parameter_values（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database)（存储过程）  
 解析并显示指定的包和环境引用的实际值  
  
 [catalog.object_parameters（SSISDB 数据库）](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database)（视图）  
 显示 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目录中所有包和项目的参数和属性，包括设计默认值和服务器默认值。  
  
 [catalog.set_execution_parameter_value（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)  
 为 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目录中的执行实例设置参数的值。  
  
 您还可以使用 **中的** “执行包” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 对话框修改参数值。 有关详细信息，请参阅 [Execute Package Dialog Box](../../2014/integration-services/execute-package-dialog-box.md)。  
  
 您还可以使用 dtexec `/Parameter` 选项修改参数值。 有关详细信息，请参阅 [dtexec Utility](packages/dtexec-utility.md)。  
  
### <a name="parameter-validation"></a>参数验证  
 如果无法解析参数值，则相应的包执行将失败。 为了帮助避免失败，您可以使用 **中的** “验证” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]对话框来验证项目和包。 通过验证，您可以确认所有参数都具有必需的值或者可以使用特定的环境引用解析必需的值。 验证还检查是否存在其他常见的包问题。  
  
 有关详细信息，请参阅 [Validate Dialog Box](catalog/validate-dialog-box.md)。  
  
### <a name="parameter-example"></a>参数示例  
 此示例介绍一个名为 **pkgOptions** 的参数，该参数用于为驻留在其中的包指定选项。  
  
 在设计时，在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中创建该参数时，默认值 1 已赋给该参数。 此默认值称为设计默认值。 如果该项目已部署到 SSISDB 目录中并且没有任何其他值赋给该参数，则在包执行期间，向与 **pkgOptions** 参数相对应的包属性赋予值 1。 在其整个生命周期中，设计默认值对于项目而言是持久的。  
  
 在准备包执行的特定实例时，值 5 将赋给 **pkgOptions** 参数。 该值称作执行值，因为仅对于该特定执行实例，该值才适用于参数。 在执行开始时，向与 **pkgOptions** 参数相对应的包属性赋予值 5。  
  
## <a name="related-tasks"></a>Related Tasks  
 [创建参数](create-parameters.md)  
  
 [在部署项目后设置参数值](../../2014/integration-services/set-parameter-values-after-the-project-is-deployed.md)  
  
## <a name="related-content"></a>相关内容  
 mattmasson.com 上的博客文章：[SSIS 快速提示：必需的参数](https://go.microsoft.com/fwlink/?LinkId=239781)。  
  
  
