---
title: 使用对象资源管理器管理对象 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.SWB.SQLSERVEROBJECTEXPLORER.DHELP
helpviewer_keywords:
- Object Explorer F1 Help
- OE F1 Help
- OE Help
ms.assetid: e60367a7-3fdd-40b8-82bb-9e819d78de5a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b78502e3bc0701af0dd662455382ce7ad2432813
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65102772"
---
# <a name="manage-objects-by-using-object-explorer"></a>使用对象资源管理器管理对象
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可以使用对象资源管理器来管理对象（如数据库、表和存储过程）。  
  
## <a name="viewing-objects-in-object-explorer"></a>在对象资源管理器中查看对象  
对象资源管理器使用树状结构将信息分组到文件夹中。 若要展开文件夹，请单击加号 (+) 或双击文件夹。 展开文件夹以显示更多详细信息。 右键单击文件夹或对象，以执行常见任务。 双击对象以执行最常见的任务。  
  
第一次展开文件夹时，对象资源管理器将查询服务器，以获取填充树的信息。 填充树时，您可以执行其他功能。 在对象资源管理器填充树时，可以单击“停止”来暂停进程。 进一步的操作（例如筛选列表）将只对文件夹的已填充部分进行操作，但刷新文件夹重新开始填充时除外。  
  
为了在存在多个对象时保留资源，对象资源管理器树中的文件夹不会自动刷新其目录列表。 若要刷新文件夹内的对象列表，请右键单击此文件夹，然后单击“刷新”。  
  
对象资源管理器最多只能显示 65,536 个对象。 可见对象超过 65,536 个以后，将无法在对象资源管理器树视图中滚动其他对象。 若要查看对象资源管理器中的其他对象，请关闭不使用的节点或使用筛选功能以减少对象数量。  
  
## <a name="filtering-the-list-of-objects-in-object-explorer"></a>在对象资源管理器中筛选对象列表  
当文件夹中包含大量对象时，可能会很难找到要查找的对象。 在此情况下，使用对象资源管理器的筛选功能可以减小列表。 例如，您可能希望在包含上百个对象的列表中找到特定的数据库用户或最近创建的表。 单击要筛选的文件夹，然后单击筛选器按钮以打开“筛选器设置”对话框。 可以按名称、创建日期、有时甚至可以按架构来筛选列表，并可提供其他筛选运算符，例如“开头为”、“包含”和“介于”。  
  
## <a name="multi-select"></a>多重选择  
在对象资源管理器中，一次只能选择一个对象。 若要选择多个项，请按 **F7** 以打开“对象资源管理器详细信息”页。 “对象资源管理器详细信息”页支持多项选择。  
  
## <a name="register-a-server-from-object-explorer"></a>从对象资源管理器中注册服务器  
连接到服务器后，即可轻松注册服务器，以供将来使用。 在对象资源管理器中，右键单击服务器名称，然后单击“注册”。 在“注册服务器”对话框中，指定要在服务器组树中放置服务器的位置。 在“服务器名称”方框中，可以使用更有意义的服务器名称替换此服务器名称。 例如，可以使用更有意义的名称（如 **Accounts Payable**）来注册服务器 **APSQL02**。  
  
## <a name="performing-actions-on-object-explorer-nodes"></a>在对象资源管理器节点上执行操作  
通过右键单击表示该对象的对象资源管理器节点，可以在对象上执行操作。 每种对象类型支持一组唯一的右键单击操作。 通过使用右键单击菜单，可以执行的操作类型包括：  
  
### <a name="open-a-connected-query-editor"></a>打开已连接的查询编辑器  
对象资源管理器连接到服务器后，可以使用对象资源管理器的连接设置打开一个新的“代码编辑器”窗口。 若要打开一个新的“代码编辑器”窗口，请在对象资源管理器中右键单击服务器名称，然后单击“新建查询”。 若要使用特定数据库打开“代码编辑器”窗口，请右键单击数据库名称，然后单击“新建查询”。 打开 Analysis Services 服务器的新查询时，可以选择 DMX、MDX 或 XMLA 查询。  
  
### <a name="start-powershell"></a>启动 PowerShell  
可通过右键单击对象资源管理器树中的大多数文件夹和对象并选择“启动 PowerShell”来启动 PowerShell 会话。 这将启动已启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 支持的 PowerShell 会话，并将路径设置为在对象资源管理器中右键单击的对象。 然后，您可以在交互式 PowerShell 环境中输入 PowerShell 命令。 有关详细信息，请参阅 [SQL Server PowerShell](https://msdn.microsoft.com/89b70725-bbe7-4ffe-a27d-2a40005a97e7)。  
  
## <a name="see-also"></a>另请参阅  
[对象资源管理器](../../ssms/object/object-explorer.md)  
[打开和配置对象资源管理器](../../ssms/object/open-and-configure-object-explorer.md)  
[从对象资源管理器连接到实例](../../ssms/object/connect-to-an-instance-from-object-explorer.md)  
[对象资源管理器详细信息窗格](../../ssms/object/object-explorer-details-pane.md)  
[Management Studio 中的自定义报告](../../ssms/object/custom-reports-in-management-studio.md)  
  
