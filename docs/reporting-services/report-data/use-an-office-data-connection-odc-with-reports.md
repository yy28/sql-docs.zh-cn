---
title: "将 Office 数据连接 (.odc) 用于报表 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Office Data Connection (.odc) files
- SharePoint integration [Reporting Services], shared data sources
- .odc files
ms.assetid: e8d6896d-f886-4390-8b5d-96f0a50c250c
caps.latest.revision: "13"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c146c2fe80f27ace8a8f03ce2767efd9751acf48
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="use-an-office-data-connection-odc-with-reports"></a>将 Office 数据连接 (.odc) 用于报表
  对于局限性方案而言，可以使用现有 Office 数据连接 (.odc) 文件来为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表提供连接信息。 在创建共享数据源时，可用 .odc 文件替代 .rsds 文件。 报表服务器使用 .odc 文件的方式与使用 .rsds 文件的方式相同；它读取文件以获得数据源类型、连接字符串以及凭据信息。  
  
 并非所有的 .odc 文件均可用于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表。 数据处理扩展插件和报表及 .odc 文件的特征决定了是否可以使用某个 .odc 文件：  
  
-   报表必须设计为与 OLE DB 或 ODBC 数据访问接口配合使用。 如果使用不同的数据处理扩展插件来创建报表，报表或其查询则可能包含 OLE DB 或 ODBC 数据提供程序所不支持的功能。  
  
-   .odc 文件必须包含所需元素和结构。 必须在文件中显式设置数据访问接口和凭据设置，以使报表服务器能够读取这些设置。 设置这些值的最佳方式是：在将 .odc 文件上载到 SharePoint 库之前将该文件导出。  
  
-   .odc 文件必须指定一个 OLE DB 或 ODBC 连接类型。  
  
-   .odc 文件必须指定一个连接字符串。  
  
-   凭据可设置为 **None**、 **Stored**或 **Integrated**。 如果将凭据方法设置为 **Stored**，则报表服务器将提示用户提供凭据，而不要使用已存储凭据。 报表服务器不能按照 .odc 文件中的定义使用已存储凭据。  
  
-   数据源所具有的架构必须与创建报表时使用的架构相同。 如果数据结构不同，报表将无法运行。  
  
-   必须在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 2007 中创建 .odc 文件（早期版本的 .odc 文件与报表定义文件不兼容）。  
  
 如果 .odc 文件指定的连接指向不能在报表服务器上进行处理的数据源，那么即便 .odc 数据源类型与支持的数据源类型相似，也不能使用该 .odc 文件。 具体而言，如果在 Microsoft Excel 2007 中创建了 .odc 文件，而该文件从 Microsoft Access、Web 或文本文件检索数据，则不能使用该 .odc 文件来为报表提供数据。  
  
 报表生成器报表和模型不能与 .odc 文件配合使用。 不能使用 .odc 文件生成模型，且不能将模型配置为使用链接到 .odc 文件的共享数据源。  
  
 如果不熟悉 .odc 文件，可以使用以下说明来创建并导出文件。 为 OLE DB 数据源创建 .odc 文件的一种简便方法就是使用 Excel 2007 和数据连接向导。 注意：向导不会创建数据源，您必须拥有已定义的外部数据源。  
  
 只有在现有 .odc 文件与报表和查询完全兼容的情况下，才能使用现有 .odc 文件。 如果遇到需要对报表或 .odc 文件进行重大修改的错误，则应为报表创建新的 .rsds 文件。 有关如何创建使用 .rsds 文件的共享数据源的详细信息，请参阅[创建和管理共享数据源（SharePoint 集成模式下的 Reporting Services）](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)。  
  
### <a name="to-create-and-export-an-odc-file"></a>创建并导出 .odc 文件  
  
1.  启动 Excel 2007。  
  
2.  在 **“数据”** 选项卡上的 **“获取外部数据”** 组中，单击 **“从其他来源”**，然后单击 **“从数据连接向导”**。  
  
3.  选择“其他/高级”，然后单击“下一步”。  
  
4.  选择 **“Microsoft OLE DB Provider for SQL Server”**，然后单击 **“下一步”**。  
  
5.  输入服务器名称（默认情况下，该名称是计算机的网络名称）和具有有效登录名及数据库权限的用户帐户。 单击 **“下一步”**。  
  
6.  选择一个数据库，然后单击 **“确定”** 以关闭 **“数据链接”** 对话框。  
  
7.  默认情况下， **“连接到特定表”** 复选框处于选中状态。 它用于从特定表检索数据。 报表服务器将忽略 .odc 文件中的所有查询，因此选中或清除该复选框均无关紧要。 检索报表数据的查询包含在报表定义文件中，而不是包含在外部文件中。  
  
8.  连接打开时，可以编辑属性并将其导出。 在 **“数据”** 选项卡的 **“连接”** 组中，单击 **“属性”**，然后单击连接名称旁边的 **“连接属性”** 按钮。  
  
9. 在 **“定义”** 选项卡上，单击 **“导出连接文件”**。  
  
10. 输入文件名，然后单击 **“保存”**。 关闭应用程序和所有打开的文件。  
  
### <a name="to-upload-and-use-an-odc-file"></a>上载并使用 .odc 文件  
  
1.  打开连接文件将要上载到其中的库。  
  
2.  在 **“上载”** 菜单中，单击 **“上载文档”**。  
  
3.  单击 **“浏览”**。  
  
4.  选择所创建的 .odc 文件。 默认情况下，.odc 文件位于“我的文档”文件夹的“我的数据源”中。  
  
5.  单击 **“打开”** 以选择该文件，单击 **“确定”** 保存选择。 新项的属性页将自动打开。  
  
6.  在“内容类型”中，选择 **“报表数据源”**，然后单击 **“确定”**。  
  
7.  指向报表。  
  
8.  单击下箭头，然后选择 **“管理数据源”**。  
  
9. 单击数据源名称。  
  
10. 如果报表使用自定义数据源信息，请单击 **“共享”**。  
  
11. 在“数据源链接”中，单击“浏览(...)”按钮。  
  
12. 选择刚上载的 .odc 文件。  
  
13. 单击 **“确定”** 以选择该文件，然后单击 **“确定”** 保存更改。  
  
     如果尝试将上述步骤用于 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库和示例报表，请注意：只有 Company Sales 报表可不经修改地立即与 .odc 文件一起使用。 其他示例报表包含有不能与 OLE DB 提供程序配合使用的查询参数和功能。 但是，如果先在报表设计器中对这些报表进行修改，那么就可以让报表与 OLE DB 访问接口配合使用。  
  
## <a name="see-also"></a>另请参阅  
 [创建、修改和删除共享数据源 (SSRS)](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)  
  
  
