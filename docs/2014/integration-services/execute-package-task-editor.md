---
title: 执行包任务编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executepackagetask.parameter.F1
- sql12.dts.designer.executepackagetask.package.f1
- sql12.dts.designer.executepackagetask.general.f1
ms.assetid: c2c96b4f-eb10-4d8b-be34-88edfd0785fb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 23dee8cac6046223bf22ea52d1ceb4013a408050
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059059"
---
# <a name="execute-package-task-editor"></a>执行包任务编辑器
  可以使用执行包任务编辑器来配置执行包任务。 执行包任务通过允许包将其他包作为工作流的组成部分运行来扩展 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的企业功能。  
  
 **您希望做什么？**  
  
-   [打开执行包任务编辑器](#open)  
  
-   [设置 "常规" 页上的选项](#general)  
  
-   [设置“包”页上的选项](#package)  
  
-   [设置“参数绑定”页上的选项](#parameter)  
  
##  <a name="open-the-execute-package-task-editor"></a><a name="open"></a>打开执行包任务编辑器  
  
1.  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中，打开包含执行包任务的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目。  
  
2.  在 SSIS 设计器中右键单击该任务，然后单击“编辑”****。  
  
##  <a name="set-the-options-on-the-general-page"></a><a name="general"></a>设置 "常规" 页上的选项  
 **名称**  
 为执行包任务提供唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **说明**  
 键入对执行包任务的说明。  
  
##  <a name="set-the-options-on-the-package-page"></a><a name="package"></a>设置 "包" 页上的选项  
 **ReferenceType**  
 为项目中的子包选择“项目引用”****。 为位于包外部的子包选择 **“外部引用”** 。  
  
> [!NOTE]  
>  “ReferenceType”**** 选项是只读的，如果包含包的项目尚未转换为项目部署模型，则该选项将设置为“外部引用”****。 有关转换的详细信息，请参阅 [将项目部署到 Integration Services 服务器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)。  
  
 **密码**  
 如果子包受密码保护，请提供子包的密码，或单击省略号按钮 (…)，为子包创建新的密码。  
  
 `ExecuteOutOfProcess`  
 指定子包是在父包的进程中运行还是在单独的进程中运行。 默认情况下，"执行包" 任务的 ExecuteOutOfProcess 属性设置为`False`，子包与父包运行在同一进程中。 如果将此属性设置为 `true`，则在单独的进程中运行子包。  这可能减慢子包的启动。 此外，如果将该属性设置为 `true`，则不能在仅工具安装中调试包；必须安装 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 产品。 有关详细信息，请参阅 [安装 Integration Services](install-windows/install-integration-services.md)。  
  
### <a name="referencetype-dynamic-options"></a>ReferenceType 动态选项  
  
#### <a name="referencetype--external-reference"></a>ReferenceType = 外部引用  
 **位置**  
 选择子包的位置。 此属性具有下表所列的选项。  
  
|Value|说明|  
|-----------|-----------------|  
|**SQL Server**|将位置设置为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例。|  
|**文件系统**|将位置设置为文件系统。|  
  
 **连接**  
 选择子包的存储位置的类型。  
  
 **PackageNameReadOnly**  
 显示包的名称。  
  
#### <a name="referencetype--project-reference"></a>ReferenceType = 项目引用  
 **PackageNameFromProjectReference**  
 选择项目中包含的要成为子包的包。  
  
### <a name="location-dynamic-options"></a>位置动态选项  
  
#### <a name="location--sql-server"></a>位置 = SQL Server  
 **连接**  
 在列表中选择一个 OLE DB 连接管理器，或\<单击 "**新建连接 ...** "> 创建新的连接管理器。  
  
 **相关主题：** [OLE DB 连接管理器](connection-manager/ole-db-connection-manager.md)、[配置 OLE DB 连接管理器](../../2014/integration-services/configure-ole-db-connection-manager.md)  
  
 **PackageName**  
 键入子包的名称，或单击省略号 (…) 再定位到包。  
  
#### <a name="location--file-system"></a>位置 = 文件系统  
 **连接**  
 在列表中选择一个文件连接管理器，或\<单击 "**新建连接 ...** "> 创建新的连接管理器。  
  
 **相关主题：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **PackageNameReadOnly**  
 显示包的名称。  
  
##  <a name="set-the-options-on-the-parameter-bindings-page"></a><a name="parameter"></a>设置 "参数绑定" 页上的选项  
 您可以将父包或项目中的值传递到子包。 项目必须使用项目部署模型，并且子包必须包含在父包所在的同一项目中。  
  
 有关将项目转换为项目部署模型的信息，请参阅 [将项目部署到 Integration Services 服务器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)。  
  
 **子包参数**  
 输入或选择子包参数的名称。  
  
 **绑定参数或变量**  
 选择包含要传递到子包的值的参数或变量。  
  
 **添加**  
 单击此选项可将参数或变量映射到子包参数。  
  
 **删除**  
 单击此选项可删除参数或变量与子包参数之间的映射。  
  
  
