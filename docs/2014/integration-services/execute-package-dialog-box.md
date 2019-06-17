---
title: 执行包对话框 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackageexecute.f1
- sql12.ssis.ssms.executepackage.f1
ms.assetid: 4f7a806d-4867-4d1f-bc65-b00c1caee7b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b4b920b17e960059e1212be7dd15c176c0b25a47
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059188"
---
# <a name="execute-package-dialog-box"></a>Execute Package Dialog Box
  使用 **“执行包”** 对话框可以运行在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器上存储的包。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包可以包含在环境变量中存储的值的参数。 在执行此类包之前，您必须指定将使用哪一环境来提供环境变量值。 一个项目可以包含多个环境，但只能使用一个环境在执行时绑定环境变量值。 如果在包中未使用任何环境变量，则不要求环境。  
  
 您希望做什么？  
  
-   [打开“执行包”对话框](#open_dialog)  
  
-   [设置“常规”页上的选项](#general)  
  
-   [设置“参数”选项卡上的选项](#parameters)  
  
-   [设置“连接管理器”选项卡上的选项](#connection)  
  
-   [设置“高级”选项卡上的选项](#advanced)  
  
-   [编写“执行包”对话框中选项的脚本](#script)  
  
##  <a name="open_dialog"></a> 打开“执行包”对话框  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器。  
  
     正在连接到承载 SSISDB 数据库的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的实例。  
  
2.  在对象资源管理器中，展开树以便显示 **“Integration Services 目录”** 节点。  
  
3.  展开 **“SSISDB”** 节点。  
  
4.  展开包含您要运行的包的文件夹。  
  
5.  右键单击该包，然后单击“执行”  。  
  
##  <a name="general"></a> 设置“常规”页上的选项  
 选择 **“环境”** 以便指定适用于运行的包的环境。  
  
##  <a name="parameters"></a> 设置“参数”选项卡上的选项  
 使用 **“参数”** 选项卡可以修改在包运行时使用的参数值。  
  
##  <a name="connection"></a> 设置“连接管理器”选项卡上的选项  
 使用“连接管理器”选项卡可以设置包连接管理器的属性。  
  
##  <a name="advanced"></a> 设置“高级”选项卡上的选项  
 使用“高级”选项卡可以管理属性和其他包设置。  
  
 “添加”  、“编辑”  、“删除”   
 单击以便添加、编辑或删除某一属性。  
  
 **日志记录级别**  
 选择用于执行包的日志记录级别。 有关详细信息，请参阅 [catalog.set_execution_parameter_value（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)。  
  
 **出错时转储**  
 指定在包执行过程中发生错误时是否创建一个转储文件。 有关详细信息，请参阅 [Generating Dump Files for Package Execution](troubleshooting/generating-dump-files-for-package-execution.md)。  
  
 **32 位运行时**  
 指定包将在 32 位系统上执行。  
  
##  <a name="script"></a> 编写“执行包”对话框中选项的脚本  
 在您处于 **“执行包”** 对话框中时，还可以使用工具栏上的 **“脚本”** 按钮为您编写 [!INCLUDE[tsql](../includes/tsql-md.md)] 代码。 生成的脚本使用与你在“执行包”  对话框中选择的相同选项调用存储过程 [catalog.start_execution（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)。 该脚本出现在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]的新脚本窗口中。  
  
  
