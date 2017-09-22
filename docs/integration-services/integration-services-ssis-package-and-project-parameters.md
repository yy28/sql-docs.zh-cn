---
title: "Integration Services (SSIS) 包和项目参数 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.parameter.f1
- sql13.dts.designer.paramterwindow.f1
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 55d240737f84e8e260222bbb921bd602d2d19062
ms.contentlocale: zh-cn
ms.lasthandoff: 09/21/2017

---
# <a name="integration-services-ssis-package-and-project-parameters"></a>Integration Services (SSIS) 包和项目参数
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) 参数可用于在包执行时向包内的属性赋值。  您可以在项目级别创建“项目参数”  ，在包级别创建“包参数”。 项目参数可用于向项目中的一个或多个包提供项目接收的任何外部输入。 利用包参数，您不必编辑和重新部署包就可以修改包执行。  
  
 在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，您使用 **Project.params** 窗口创建、修改或删除项目参数。 通过使用 **设计器中的** “参数” [!INCLUDE[ssIS](../includes/ssis-md.md)] 选项卡来创建、修改和删除包参数。 通过使用 **“参数化”** 对话框，您可以将新的或现有的参数与任务属性相关联。 有关使用 **Project.params** 窗口和 **“参数”** 选项卡的详细信息，请参阅 [Create Parameters](http://msdn.microsoft.com/library/cd5d675b-dd5d-49cc-8b1f-dc717a973f99)。 有关 **“参数化”** 对话框的详细信息，请参阅 [Parameterize Dialog Box](http://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350)。  
  
## <a name="parameters-and-package-deployment-model"></a>参数和包部署模型  
 如果您正在使用包部署模型部署包，通常应使用配置而非参数。  
  
 使用包部署模型部署包含参数的包然后执行包时，在执行期间不调用参数。 如果包中包含包参数和表达式，则在运行时应用生成的值。 如果包中包含项目参数，则包执行可能会失败。  
  
## <a name="parameters-and-project-deployment-model"></a>参数和项目部署模型  
 将项目部署到 Integration Services (SSIS) 服务器时，你使用视图、存储过程和 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] UI 来管理项目和包参数。 有关详细信息，请参阅以下主题。  
  
-   [视图 &#40; Integration Services 目录 &#41;](../integration-services/system-views/views-integration-services-catalog.md)  
  
-   [存储过程 &#40; Integration Services 目录 &#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
  
-   [“配置”对话框](../integration-services/service/configure-dialog-box.md)  
  
-   [Execute Package Dialog Box](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)  
  
### <a name="parameter-values"></a>参数值  
 可以为参数最多赋予三个不同类型的值。 当启动包执行时，将单个值用于参数，然后将参数解析为最终的文字值。  
  
 下表列出了值的类型。  
  
|值名称|说明|值的类型|  
|----------------|-----------------|-------------------|  
|执行值|针对包执行的特定实例赋予的值。 此赋值将覆盖所有其他值，但仅应用于包执行的单个实例。|文字|  
|服务器值|在将项目部署到 Integration Services 服务器后在项目范围内赋予参数的值。 此值将覆盖设计默认值。|文字或环境变量引用|  
|设计值|在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中创建或编辑项目时赋予参数的值。 该值对于项目而言是持久的。|文字|  
  
 可以使用单个参数向多个包属性分配值。 只能从单个参数为单个包属性分配值。  
  
###  <a name="executions"></a> 执行和参数值  
  “执行”是表示包执行的单个实例的对象。 当您创建执行时，指定运行包所需的所有详细信息（如执行参数值）。 您还可以修改现有执行的参数值。  
  
 显式设置一个执行参数值时，该值仅适用于执行的特定实例。 使用执行值而非服务器值或设计值。 如果未显式设置执行值并指定了服务器值，则使用服务器值。  
  
 某一参数标记为必需时，必须为该参数指定服务器值或执行值。 否则，不会执行相应的包。 尽管该参数在设计时具有默认值，但在部署项目后，将永远不会再使用该默认值。  
  
#### <a name="environment-variables"></a>环境变量  
 如果某个参数引用某一环境变量，则来自该变量的文字值通过指定的环境引用进行解析并且应用于该参数。 用于包执行的最终的文字参数值称作执行参数值。 使用 **“执行”** 对话框来指定执行的环境引用  
  
 如果项目参数引用某一环境变量且无法在执行时解析来自该变量的文字值，则使用设计值。 不使用服务器值。  
  
 要查看分配给参数值的环境变量，请查询 catalog.object_parameters 视图。 有关详细信息，请参阅[catalog.object_parameters &#40;SSISDB 数据库 &#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md).  
  
#### <a name="determining-execution-parameter-values"></a>确定执行参数值  
 下面的 Transact-SQL 视图和存储过程可用于显示和设置参数值。  
  
 [catalog.execution_parameter_values &#40;SSISDB 数据库 &#41;](../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)(view)  
 显示特定执行将使用的实际参数值  
  
 [catalog.get_parameter_values &#40;SSISDB 数据库 &#41;](../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md) （存储过程）  
 解析并显示指定的包和环境引用的实际值  
  
 [catalog.object_parameters &#40;SSISDB 数据库 &#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) (view)  
 显示 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目录中所有包和项目的参数和属性，包括设计默认值和服务器默认值。  
  
 [catalog.set_execution_parameter_value &#40;SSISDB 数据库 &#41;](../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 为 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目录中的执行实例设置参数的值。  
  
 您还可以使用 **中的** “执行包” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 对话框修改参数值。 有关详细信息，请参阅 [Execute Package Dialog Box](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)。  
  
 您还可以使用 dtexec **/Parameter** 选项修改参数值。 有关详细信息，请参阅 [dtexec Utility](../integration-services/packages/dtexec-utility.md)。  
  
### <a name="parameter-validation"></a>参数验证  
 如果无法解析参数值，则相应的包执行将失败。 为了帮助避免失败，您可以使用 **中的** “验证” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]对话框来验证项目和包。 通过验证，您可以确认所有参数都具有必需的值或者可以使用特定的环境引用解析必需的值。 验证还检查是否存在其他常见的包问题。  
  
 有关详细信息，请参阅 [Validate Dialog Box](../integration-services/service/validate-dialog-box.md)。  
  
### <a name="parameter-example"></a>参数示例  
 此示例介绍一个名为 **pkgOptions** 的参数，该参数用于为驻留在其中的包指定选项。  
  
 在设计时，在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中创建该参数时，默认值 1 已赋给该参数。 此默认值称为设计默认值。 如果该项目已部署到 SSISDB 目录中并且没有任何其他值赋给该参数，则在包执行期间，向与 **pkgOptions** 参数相对应的包属性赋予值 1。 在其整个生命周期中，设计默认值对于项目而言是持久的。  
  
 在准备包执行的特定实例时，值 5 将赋给 **pkgOptions** 参数。 该值称作执行值，因为仅对于该特定执行实例，该值才适用于参数。 在执行开始时，向与 **pkgOptions** 参数相对应的包属性赋予值 5。  
  
## <a name="create-parameters"></a>Create Parameters
使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 可以创建项目参数和包参数。 下面的过程提供了有关创建包参数/项目参数的分步说明。  
  
> **注意：**若要将使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的早期版本创建的项目转换为项目部署模型，则可以使用“Integration Services 项目转换向导”来创建基于配置的参数。 有关详细信息，请参阅[部署 Integration Services (SSIS) 项目和包](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)。  
  
### <a name="create-package-parameters"></a>创建包参数  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中打开包，然后在 SSIS 设计器中单击 **“参数”** 选项卡。  
  
     ![包参数选项卡](../integration-services/media/denali-package-parameters.gif "包参数选项卡")  
  
2.  单击工具栏上的 **“添加参数”** 按钮。  
  
     ![添加工具栏按钮](../integration-services/media/denali-parameter-add.gif "添加工具栏按钮")  
  
3.  为列表自身中或 **“属性”**窗口中的 **“名称”**、 **“数据类型”**、 **“值”**、 **“敏感”** 和 **“必需”** 属性输入值。 下表对这些属性进行了说明：  
  
    |属性|Description|  
    |--------------|-----------------|  
    |“属性”|参数名。|  
    |“名称”|参数的数据类型。|  
    |默认值|在设计时分配的参数的默认值。 这也称为设计默认值。|  
    |“值”|敏感参数值在目录中加密，并且在使用 Transact-SQL 或 SQL Server Management Studio 查看时以 NULL 值的形式出现。|  
    |必需|需要首先指定并非设计默认值的值，包才能执行。|  
    |Description|出于可维护性目的而提供的参数的说明。 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，当在适用的参数窗口中选择参数时，在“Visual Studio 属性”窗口中设置参数说明。|  
  
    > **注意：**在向目录部署某一项目时，还有几个属性将与该项目相关联。 若要查看目录中所有参数的全部属性，请使用 [catalog.object_parameters（SSISDB 数据库）](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)视图。  
  
4.  保存项目以保存对参数所做的更改。 参数值将存储在项目文件中。  
  
    > **警告!!** 可以直接在列表中编辑，也可以使用“属性”窗口来修改参数属性的值。 可以使用“删除 (X)”工具栏按钮来删除参数。 使用最后一个工具栏按钮，可以为仅在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中执行包时使用的参数指定值。  
  
    > **注意：**如果未在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中打开项目便重新打开包文件，则“参数”选项卡将为空且被禁用。  
  
### <a name="create-project-parameters"></a>创建项目参数  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中打开该项目。  
  
2.  在解决方案资源管理器中右键单击“Project.params”，然后单击“打开”，或者双击“Project.params”将其打开。  
  
     ![项目参数窗口](../integration-services/media/denali-project-parameters.gif "项目参数窗口")  
  
3.  单击工具栏上的 **“添加参数”** 按钮。  
  
     ![添加工具栏按钮](../integration-services/media/denali-parameter-add.gif "添加工具栏按钮")  
  
4.  为 **“名称”**、 **“数据类型”**、 **“值”**、 **“敏感”**和 **“必需”** 属性输入值。  
  
    |属性|Description|  
    |--------------|-----------------|  
    |“属性”|参数名。|  
    |“名称”|参数的数据类型。|  
    |默认值|在设计时分配的参数的默认值。 这也称为设计默认值。|  
    |“值”|敏感参数值在目录中加密，并且在使用 Transact-SQL 或 SQL Server Management Studio 查看时以 NULL 值的形式出现。|  
    |必需|需要首先指定并非设计默认值的值，包才能执行。|  
    |Description|出于可维护性目的而提供的参数的说明。 在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，当在适用的参数窗口中选择参数时，在“Visual Studio 属性”窗口中设置参数说明。|  
  
5.  保存项目以保存对参数所做的更改。 参数值将存储在项目文件的配置中。 保存项目文件以将对参数值的所有更改提交到磁盘。  
  
    > **警告!!!** 可以直接在列表中编辑，也可以使用“属性”窗口来修改参数属性的值。 可以使用“删除 (X)”工具栏按钮来删除参数。 使用最后一个工具栏按钮打开 **“管理参数值”** 对话框，您可以为仅在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中执行包时使用的参数指定值。  
    
## <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
**参数化**对话框，可以将新的或现有参数与任务的属性相关联。 通过右键单击任务或中的控制流选项卡中打开对话框 [！包括[ssIS](/sql-docs/docs/integration-services/integration-services-ssis-package-and-project-parameters)。
  
### <a name="options"></a>选项  
 **属性**  
 选择要与参数相关联的任务属性。 此列表包含可参数化的所有属性。  
  
 **使用现有的参数**  
 使用此选项可将任务属性与某个现有参数相关联，从而可以从下拉列表中选择该参数。  
  
 **不使用参数**  
 选择此选项可以删除对参数的引用。 不删除该参数。  
  
 **创建新的参数**  
 选择此选项可创建要与任务属性相关联的新参数。  
  
 **名称**  
 指定要创建的参数的名称。  
  
 **Description**  
 指定参数的说明。  
  
 **值**  
 指定参数的默认值。 这也称作设计默认值，以后在部署时可以覆盖该值。  
  
 **范围**  
 通过选择“项目”或“包”选项指定参数的范围。 项目参数可用于向项目中的一个或多个包提供项目接收的任何外部输入。 利用包参数，您不必编辑和重新部署包就可以修改包执行。  
  
 **敏感**  
 通过选中或清除该复选框，指定参数是否为敏感参数。 敏感参数值在目录中加密，并且在使用 Transact-SQL 或 SQL Server Management Studio 查看时以 NULL 值的形式出现。  
  
 **必需**  
 指定参数是否要求在执行包之前指定设计默认值之外的值。  
 
## <a name="set-parameter-values-after-the-project-is-deployed"></a>部署项目后设置参数值
通过部署向导，您可以在将项目部署到目录时设置服务器默认参数值。 在您的项目处于目录中后，您可以使用 SQL Server Management Studio (SSMS) 对象资源管理器或 Transact-SQL 来设置服务器默认值。  
  
### <a name="set-server-defaults-with-ssms-object-explorer"></a>使用 SSMS 对象资源管理器设置服务器默认值  
  
1.  选择并右键单击“集成服务”节点下的项目。  
  
2.  单击 **“属性”** 以便打开 **“项目属性”** 对话框窗口。  
  
3.  通过在 **“选择页”** 之下单击 **“参数”**，打开参数页。  
  
4.  在 **“参数”** 列表中选择所需参数。 注意： **“容器”** 列将帮助区分项目参数和包参数。  
  
5.  在 **“值”** 列中，指定所需的服务器默认参数值。  

### <a name="set-server-defaults-with-transact-sql"></a>使用 TRANSACT-SQL 设置服务器默认值  
 若要使用 TRANSACT-SQL 设置服务器默认值，请使用 [catalog.set_object_parameter_value（SSISDB 数据库）](../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md)存储过程。 若要查看当前服务器默认值，请查询 [catalog.object_parameters（SSISDB 数据库）](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)视图。 若要清除服务器默认值，请使用 [catalog.clear_object_parameter_value（SSISDB 数据库）](../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md)存储过程。  
  
## <a name="related-content"></a>相关内容  
 mattmasson.com 上的博客文章 [SSIS 快速提示：必需参数](http://go.microsoft.com/fwlink/?LinkId=239781)。  
  
  
