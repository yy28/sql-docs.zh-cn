---
title: 配置 SSIS 日志对话框的 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.configuredtslogs.loggingdetails.f1
- sql12.dts.designer.configuredtslogs.providersandlogs.f1
- sql12.dts.designer.configuredtslogs.containers.f1
helpviewer_keywords:
- Configure SSIS Logs dialog box
ms.assetid: 4b980275-cd9a-4943-8c36-727d51f9a484
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dbba1b7712bcbdccc821e419b3101065c3164913
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375206"
---
# <a name="configure-ssis-logs-dialog-box"></a>“配置 SSIS 日志”对话框
  使用 **“配置 SSIS 日志”** 对话框可以定义包的日志记录选项。  
  
 **您希望做什么？**  
  
1.  [打开“配置 SSIS 日志”对话框](#open_dialog)  
  
2.  [配置“容器”窗格中的选项](#container)  
  
3.  [配置“提供程序和日志”选项卡上的选项](#provider)  
  
4.  [配置“详细信息”选项卡上的选项](#detail)  
  
##  <a name="open_dialog"></a> 打开“配置 SSIS 日志”对话框  
 **打开“配置 SSIS 日志”对话框**  
  
-   在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器的 **SSIS** 菜单上，单击 **“日志记录”** 。  
  
##  <a name="container"></a> 配置“容器”窗格中的选项  
 可以使用 **“配置 SSIS 日志”** 对话框的 **“容器”** 窗格，为包及其容器启用日志记录。  
  
### <a name="options"></a>选项  
 **“配置 SSIS 日志”**  
 选中层次结构视图中的该复选框可以为日志记录启用包和包容器：  
  
-   如果清除此复选框，则不会为日志记录启用容器。 选中此复选框将启用日志记录。  
  
-   如果此复选框为灰色，则容器将使用其父容器的日志记录选项。 此选项对包不可用。  
  
-   如果选中此复选框，那么容器将定义自己的日志记录选项。  
  
 如果容器为灰色，而您想要设置该容器的日志记录选项，请单击对应复选框两次。 第一次单击将清除该复选框，第二次单击将选中该复选框，这样您就可以选择要使用的日志提供程序以及要记录的信息。  
  
##  <a name="provider"></a> 配置“提供程序和日志”选项卡上的选项  
 可以使用“配置 SSIS 日志”对话框的“提供程序和日志”选项卡，创建和配置用于捕获运行时事件的日志。  
  
### <a name="options"></a>选项  
 **提供程序类型**  
 从列表中选择日志提供程序的类型。  
  
 **“添加”**  
 将指定类型的日志添加到包的日志提供程序集合中。  
  
 **名称**  
 通过使用复选框，可以为在“配置 SSIS 日志”对话框的“容器”窗格中选择的容器或任务启用或禁用日志。 名称字段是可编辑的。 可以使用提供程序的默认名称，也可以键入唯一的描述性名称。  
  
 **说明**  
 说明字段是可编辑的。 可以单击该字段，然后修改日志的默认说明。  
  
 **Configuration**  
 在列表中选择一个现有的连接管理器或单击\<“新建连接...”> 以创建新的连接管理器。 根据日志提供程序的类型，您可以配置 OLE DB 连接管理器或文件连接管理器。 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 事件日志的日志提供程序不需要任何连接。  
  
 相关主题：[OLE DB 连接管理器](connection-manager/ole-db-connection-manager.md)管理器中，[文件连接管理器](connection-manager/file-connection-manager.md)  
  
 **删除**  
 选择一个日志提供程序，然后单击“删除”。  
  
##  <a name="detail"></a> 配置“详细信息”选项卡上的选项  
 可以使用 **“配置 SSIS 日志”** 对话框的 **“详细信息”** 选项卡，指定要启用日志记录的事件以及要记录的详细信息。 所选的信息适用于包中的所有日志提供程序。 例如，无法将一些信息写入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，而在文本文件中写入另外一些信息。  
  
### <a name="options"></a>选项  
 **事件**  
 为事件启用或禁用日志记录功能。  
  
 **说明**  
 查看事件的说明。  
  
 **高级**  
 选中或清除要记录的事件，以及选中或清除要为每个事件记录的信息。 单击 **“基本”** 可以隐藏除事件列表之外的所有日志记录详细信息。 日志记录可以包含以下信息：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**Computer**|发生所记录事件的计算机的名称。|  
|**“运算符”**|启动包的人员的用户名。|  
|**SourceName**|发生所记录事件的包、容器或任务的名称。|  
|**SourceID**|发生所记录事件的包、容器或任务的全局唯一标识符 (GUID)。|  
|**ExecutionID**|包执行实例的全局唯一标识符。|  
|**MessageText**|与日志项关联的消息。|  
|**DataBytes**|保留供将来使用。|  
  
 **“基本”**  
 选中或清除要记录的事件。 选择此选项将隐藏除事件列表之外的日志记录详细信息。 默认情况下，如果选择某事件，则会为该事件选择所有日志记录详细信息。 单击 **“高级”** 将显示所有日志记录详细信息。  
  
 **加载**  
 指定要用作设置日志记录选项的模板的现有 XML 文件。  
  
 **保存**  
 将配置详细信息以模板形式保存到 XML 文件。  
  
  
