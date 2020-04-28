---
title: 创建连接管理器 |Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.connectionmanager.f1
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- packages [Integration Services], connections
- connection managers [Integration Services], creating
- SQL Server Integration Services packages, connections
ms.assetid: 6ca317b8-0061-4d9d-b830-ee8c21268345
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ed61dbba038068b8584d8d73893e48adb832683b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176477"
---
# <a name="create-connection-managers"></a>创建连接管理器
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含多种连接管理器以满足连接不同类型的服务器和数据源的任务的需要。 在不同类型的数据存储中提取和加载数据的数据流组件，以及将日志写入服务器、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 表或文件的日志提供程序，都使用连接管理器。 例如，具有发送邮件任务的包使用 SMTP 类型的连接管理器来连接到简单邮件传输协议 (SMTP) 服务器。 具有执行 SQL 任务的包可以使用 OLE DB 连接管理器来连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库。 有关详细信息，请参阅 [Integration Services (SSIS) 连接](connection-manager/integration-services-ssis-connections.md)。

 若要在创建新包时自动创建和配置连接管理器，可以使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导。 该向导还有助于创建和配置使用连接管理器的源和目标。 有关详细信息，请参阅 [Create Packages in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md)。

 若要手动创建新的连接管理器并将其添加到现有包，可以使用在 **设计器的** “控制流” **、**“数据流” **和**“事件处理程序” **选项卡上出现的** “连接管理器” [!INCLUDE[ssIS](../includes/ssis-md.md)] 区域。 从 **“连接管理器”** 区域，选择要创建的连接管理器的类型，并使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器提供的对话框设置连接管理器的属性。 有关详细信息，请参阅本主题后面的“使用连接管理器区域”部分。

 将连接管理器添加到包之后，可以在任务、Foreach 循环容器、源、转换和目标中使用它。 有关详细信息，请参阅 [Integration Services 任务](control-flow/integration-services-tasks.md)、[Foreach 循环容器](control-flow/foreach-loop-container.md)和[数据流](data-flow/data-flow.md)。

## <a name="using-the-connection-managers-area"></a>使用连接管理器区域
 可以在 **设计器的**“控制流” **、**“数据流” **或** “事件处理程序” [!INCLUDE[ssIS](../includes/ssis-md.md)] 选项卡活动时创建连接管理器。

 以下关系图显示 **设计器的** “控制流” **选项卡上的** “连接管理器” [!INCLUDE[ssIS](../includes/ssis-md.md)] 区域。

 ![具有包的控制流设计器的屏幕快照](media/samplecontrolflow.gif "具有包的控制流设计器的屏幕快照")

#### <a name="to-add-configure-or-delete-a-connection-manager-in-ssis-designer"></a>在 SSIS 设计器中添加、配置或删除连接管理器

-   [在包中添加、删除或共享连接管理器](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)

-   [设置连接管理器的属性](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)

## <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>用于连接管理器的 32 位和 64 位提供程序
 连接管理器所使用的很多提供程序都有 32 位和 64 位版本。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 设计环境是 32 位环境，设计包时您只能看到 32 位提供程序。 因此，如果还安装了同一个提供程序的 32 位版本，则只能将连接管理器配置为使用特定的 64 位提供程序。

 在运行时，系统将使用正确的版本，即使在设计时指定了 32 位版本的提供程序也没有关系。 即使包运行在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，也可以运行 64 位版本的提供程序。

 两种版本的提供程序都有相同的 ID。 若要指定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 运行时是否使用可用的 64 位版本的提供程序，需要设置 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目的 Run64BitRuntime 属性。 如果 Run64BitRuntime 属性设置为`true`，则运行时会查找并使用64位提供程序;如果 Run64BitRuntime 为`false`，则运行时会查找并使用32位提供程序。 有关可以对 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目进行设置的属性的详细信息，请参阅 [Integration Services (SSIS) 与 Studio 环境](integration-services-ssis-development-and-management-tools.md)。

## <a name="see-also"></a>另请参阅
 [&#40;SSIS&#41; 事件处理程序](integration-services-ssis-event-handlers.md)的[控制流](control-flow/control-flow.md)[数据流](data-flow/data-flow.md)Integration Services


