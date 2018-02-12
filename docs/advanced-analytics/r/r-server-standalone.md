---
title: "R Server（独立版）| Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
vms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: ca9e48f1-67b8-4905-9b78-56752d7a4e81
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 3f0c567463c25a54829a988516890bead171f5ec
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="r-server-standalone"></a>R Server (Standalone)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Microsoft 发布了 SQL Server 2016 中**R Server （独立）**，作为其平台，用于支持企业级的分析的一部分。  Microsoft R Server R 语言中，提供可伸缩性和安全性和地址的内存中限制的开放源代码。SQL Server R Services，如 Microsoft R Server （独立） 提供了并行和分块处理的数据，使 R 用户能够使用比适合在内存中得更大的数据。

在 SQL Server 自 2017 年，已为享用学习，机社区中广泛的支持和包括的文本分析和深入学习的常用库的 Python 语言添加支持。  以反映此广泛的语言，我们已也已重命名到**Microsoft 机器学习 Server （独立）**。

## <a name="benefits-of-microsoft-r-server"></a>Microsoft R Server 的优点

为分布式计算多个平台上，可以使用 Microsoft R Server。 从 SQL Server 安装程序安装时，你将发布和部署模型中获取基于 Windows 的服务器和所有所需的工具。 有关其他平台的详细信息，请参阅 MSDN 库中的以下资源：

+ [Microsoft R Server 简介](https://msdn.microsoft.com/microsoft-r/rserver)
+ [R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)

你还可以安装 Microsoft R Server 作为开发客户端，用于获取 RevoScaleR 库和创建可以部署到 SQL Server 的 R 解决方案所需的工具。

## <a name="whats-new-in-microsoft-machine-learning-server"></a>什么是 Microsoft 机器学习 Server 中的新增功能

如果你安装使用 SQL Server 2017 安装程序的机器学习服务 （独立版），你现在可以选择要添加的 Python 语言。 当然，R 语言仍然是受支持的选项，并且如果需要，甚至可以安装这两种语言。
 
在 SQL Server 自 2017 年 1 CTP 2.0 中，服务器安装还包括 mrsdeploy 包以及用于实现模型的其他实用工具。 有关详细信息，请参阅[与 mrsdeploy 操作化](../../advanced-analytics/operationalization-with-mrsdeploy.md)。

SQL Server 机器学习的企业用户可以使用的可下载 Microsoft R Server 安装程序升级其调用绑定进程中的 R 组件。 有关详细信息，请参阅[使用 SqlBindR 升级和 SQL Server 实例](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

## <a name="get-microsoft-r-server-or-machine-learning-server-standalone"></a>获取 Microsoft R Server 或机器学习 Server （独立）

 有安装 Microsoft R Server 的多个选项：

+ 使用 SQL Server 安装向导

  [创建 R Server（独立版）](../r/create-a-standalone-r-server.md)

  运行 SQL Server 2016 安装程序以安装**Microsoft R Server （独立）**。 默认情况下添加 R 语言。
  或者，运行 SQL Server 2017 安装程序以安装**机器学习 Server （独立）**并选择 R 和 / 或 Python。

  > [!IMPORTANT]
  > 安装服务器的选项处于**共享功能**的安装程序的部分。 不安装任何其他组件。
  >
  > 最好是不要其中已安装 SQL Server R Services 或 SQL Server 计算机学习 Services 的计算机上安装服务器。

+ 命令行选项用于 SQL Server 安装程序

  [从命令行安装 Microsoft R Server](../r/install-microsoft-r-server-from-the-command-line.md)

  SQL Server 安装程序支持通过一组丰富的命令行自变量的无人参与的安装。

+ 使用独立安装程序

  [运行适用于 Windows 的 Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。

  你现在可以使用新的 Windows installer 安装设置的 Microsoft R Server 或 Microsoft 机器学习 Server 的新实例。  Microsoft R Server （和 Microsoft 机器学习服务器） 需要 SQL Server Enterprise 协议。 但是，在运行独立安装程序后，现有安装的支持策略将更新，为使用新的现代生命周期策略。 此支持选项可确保更频繁地比起在使用 SQL Server 服务版本时应用的机器学习组件更新。

  
+ 升级 SQL Server 实例

  [使用 SqlBindR R Services 的实例升级](./use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。
  
  你可以使用独立安装程序升级 SQL Server 2016 R Services 以使用键。 最新版本的实例当你运行安装程序时，现代生命周期支持策略将应用到服务器，并且 R 组件将收到更频繁的更新。
  
  > [!请注意} 此更新方法目前仅适用于 SQL Server 2016 的现有安装。 但是，升级将支持为 SQL Server 2017 在将来。

## <a name="related-machine-learning-products"></a>相关的机器学习产品

+ 使用 R Server 的 azure 虚拟机

  [设置 R Server 虚拟机](../../advanced-analytics/r-services/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
  Azure 应用商店包括包括 R Server 的多个虚拟机映像。 在 Microsoft Azure 中创建新的 R Server 虚拟机是设置服务器以在开发和部署预测模型中使用的最快方法。 映像附带的缩放和共享已配置，它可以轻松将应用程序内的 R 分析，并且可以将 R 集成与后端系统的功能。

+ 数据科学虚拟机

  [数据科学虚拟机-Windows 2016 Preview](http://aka.ms/dsvm/win2016)

  数据科学虚拟机的最新版本包括 R Server，SQL Server，以及用于机器学习中，最常用的工具的一个数组所有预安装和测试。 创建 Jupyter 笔记本、 Julia 中开发解决方案和使用 MXNet、 CNTK，等 TensorFlow GPU 启用深入学习库。

## <a name="resources"></a>Resources

有关示例、 教程和 Microsoft R Server 有关的详细信息，请参阅[Microsoft R 产品](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started)。

## <a name="see-also"></a>另请参阅

 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)

