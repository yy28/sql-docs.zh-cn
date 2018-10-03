---
title: 创建并在管理中心配置 PowerPivot 服务应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b2e5693e-4af3-453f-83f3-07481ab1ac6a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac1b7ad9e5308437dacf51b7960822e7636ab3e9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168977"
---
# <a name="create-and-configure-a-powerpivot-service-application-in-central-administration"></a>在管理中心中创建和配置 PowerPivot 服务应用程序
  PowerPivot 服务应用程序是 PowerPivot 系统服务的共享服务实例。 每个服务应用程序都具有自己的应用程序标识、配置设置、属性和内部数据存储。  
  
 本主题包含以下各节：  
  
 [确定是否创建新的 PowerPivot 服务应用程序](#determine)  
  
 [创建 PowerPivot 服务应用程序](#CreateApp)  
  
 [配置 PowerPivot 服务应用程序](#ConfigApp)  
  
 [将分配到 Web 应用程序的 PowerPivot 服务应用程序](#AssignGSA)  
  
 [编辑服务应用程序属性](#EditGSA)  
  
##  <a name="determine"></a> 确定是否创建新的 PowerPivot 服务应用程序  
 PowerPivot for SharePoint 安装必须在场中具有至少一个 PowerPivot 服务应用程序。 如果您使用了 PowerPivot 配置工具来配置服务器，则会自动创建服务应用程序。 否则，您必须在管理中心手动创建 PowerPivot 服务应用程序。  
  
 创建服务应用程序将使该服务可用并生成服务应用程序数据库。 根据您在创建服务应用程序时选择的选项，PowerPivot 服务连接将添加到默认的服务连接组中。 订阅默认服务连接组的所有 SharePoint Web 应用程序都将自动获得对 PowerPivot 服务应用程序的直接访问权限。  
  
 您可以创建多个 PowerPivot 服务应用程序。 尽管一个服务应用程序对大多数部署方案就足够了，但如果您的业务具有如下要求，则可能要考虑创建附加的 PowerPivot 服务应用程序：  
  
-   为每个应用程序使用不同的无人参与的 PowerPivot 数据刷新帐户。  
  
-   使用不同的超时、使用情况历史记录以及用于查询响应报告的阈值。  
  
-   将服务管理委托给不同的人士。 管理员将看到数据刷新历史记录、使用情况数据以及仅限于其管理的应用程序的其他属性。 如果要求您隔离 SharePoint Web 应用程序（例如，如果您的公司提供宿主服务，该服务必须确保为属于不同客户的 SharePoint Web 应用程序进行数据隔离），则创建单独的 PowerPivot 服务应用程序可通过确保每个服务管理员仅看到其所管理的应用程序的配置设置和属性，帮助满足隔离要求。  
  
 创建附加的服务应用程序为管理服务关联引入了新的要求。 也就是说，将要求您为您创建的每个附加的服务应用程序都创建和使用自定义的服务关联列表。  
  
 如果您没有明确的理由需要创建附加的 PowerPivot 服务应用程序，则应使用单个服务应用程序来用于场中的所有 Web 应用程序。  
  
##  <a name="CreateApp"></a> 创建 PowerPivot 服务应用程序  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  在 **“服务应用程序”** 功能区中，单击 **“新建”**。  
  
3.  选择**SQL Server PowerPivot 服务应用程序**。 如果该服务未在列表中出现，则表示 PowerPivot for SharePoint 未安装或者配置不正确。  
  
4.  在中**创建新 PowerPivot 服务应用程序**页上，输入应用程序的名称。 默认值是 PowerPivotServiceApplication\<编号 >。 如果您创建多个 PowerPivot 服务应用程序，则说明性的名称将有助于其他管理员理解应用程序的使用方式。  
  
5.  在“应用程序池”中，为该应用程序创建一个新的应用程序池（推荐）。 为该应用程序池选择或创建一个托管帐户。 请确保指定一个域用户帐户。 通过域用户帐户，可以使用 SharePoint 的托管帐户功能，从而使您可以在一个位置中更新密码和帐户信息。 如果您计划扩展部署以便包括将在同一标识下运行的附加服务实例，则域帐户是必需的。  
  
6.  在 **“数据库服务器”** 中，默认值是承载场配置数据库的 SQL Server 数据库引擎实例。 您可以使用该服务器或者选择其他的 SQL Server。  
  
7.  在中**数据库名称**，默认值是 PowerPivotServiceApplication1_\<guid >。 您必须为每个 PowerPivot 服务应用程序都创建唯一的数据库。 默认数据库名称对应于服务应用程序的默认名称。 如果您输入了唯一的服务应用程序名称，则遵循您的数据库名称的类似命名约定，以便可以一起管理它们。  
  
8.  在 **“数据库身份验证”** 中，默认值是 “Windows 身份验证”。 如果您选择 **“SQL 身份验证”**，请参考 SharePoint 管理员指南以便了解有关如何在 SharePoint 部署中使用此身份验证类型的最佳实践。  
  
9. （可选） 选中的复选框**添加到服务器场的默认代理组此 PowerPivot 服务应用程序代理。** 这会将该服务应用程序连接添加到默认服务连接组。  
  
     如果您在创建第一个 PowerPivot 服务应用程序，则必须选中此复选框。 默认连接组中必须有一个 PowerPivot 服务应用程序，以便确保 PowerPivot 管理面板正确工作。  
  
     如果默认连接组中已存在一个 PowerPivot 服务应用程序，则不要再向其中添加 PowerPivot 服务应用程序。 添加同一服务应用程序类型的多个条目是不支持的配置并且可能导致错误。 如果您在创建附加的服务应用程序，则应将它们保留在默认连接组外并且将它们添加到自定义列表中。  
  
     有关服务关联的详细信息，请参阅[PowerPivot 服务应用程序连接到管理中心中的 SharePoint Web 应用程序](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)。  
  
10. 单击“确定” **。** 。该服务将在场的服务应用程序列表中与其他托管服务显示在一起。  
  
##  <a name="ConfigApp"></a> 配置 PowerPivot 服务应用程序  
 PowerPivot 服务应用程序使用默认配置创建。 对于大多数情况，建议您采用这些默认设置。 仅在您遇到响应时间较长或删除的连接时，或者您在为特定的 SharePoint Web 应用程序改变 PowerPivot 服务配置时，才更改这些默认设置。  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
     在服务应用程序列表中，您应该看到刚创建和命名的服务应用程序。 默认名称是 **PowerPivotServiceApplication1**。  
  
2.  单击 PowerPivot 服务应用程序。 这将打开 PowerPivot 管理面板。  
  
3.  在面板右上角的 **“操作”** 列表中，单击 **“配置服务应用程序设置”**。  
  
4.  在中**数据库加载超时**，增加或减少值可以更改 PowerPivot 服务等待来自它将加载数据请求转发到 SQL Server Analysis Services (PowerPivot) 实例的响应的时间长度。 因为非常大的数据集需要花时间在线路上移动，所以必须确保 PowerPivot 服务实例有充裕的时间检索 Excel 工作簿并将 PowerPivot 数据移到 Analysis Services 实例以便进行查询处理。 因为 PowerPivot 数据可能会非常大，所以默认值为 30 分钟。  
  
5.  在 **“连接池超时”** 中，增加或减少值可以更改空闲数据连接保持打开状态的分钟数。 默认值为 30 分钟。 在此期间中，对于来自相同 PowerPivot 数据的同一 SharePoint 用户的只读请求，PowerPivot 服务将重用空闲数据连接。 如果在指定的时段中没有收到针对该数据的进一步的请求，则从池中删除该连接。 有效值为 1 至 3600 秒。 有关连接池的详细信息，请参阅[配置设置参考&#40;PowerPivot for SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)。  
  
6.  在中**最大用户连接池大小**，增加或减少值可以更改 PowerPivot 服务将在单独的连接池中为每个 SharePoint 用户、 PowerPivot 数据集创建的空闲连接的最大数目和版本组合。  
  
     默认值为 1000 个空闲连接。 有效值为 -1（无限制）、0（禁用用户连接池）或 1 到 10000。  
  
     这些连接池使服务能够更有效地支持由同一用户建立的与相同只读数据的持续连接。 如果您禁用了连接池，将重新创建每个连接。  
  
     请注意，更改对连接池大小的限制（包括将其设置为 0）不会导致删除连接。 连接池存在的目的是减少连接数据时需要等待的时间。 PowerPivot 服务将永远不会拒绝基于连接池设置的连接。  
  
7.  在中**最大管理连接池大小**，增加或减少值可以更改连接池中为 PowerPivot 服务连接到 Analysis Services 创建的打开连接的数目。 每个 PowerPivot 服务实例都打开与同一计算机上的 Analysis Services 实例的单独管理连接。 PowerPivot 服务创建一个单独的池以便出于检查空闲连接和监视服务器运行状况的目的而重用管理连接。 默认值为 200 个连接。 有效值为 -1（无限制）、0（禁用管理连接池）或 1 到 100。 如果您选择 0，将重新创建每个连接。  
  
8.  在中**分配方法**，可以指定负载平衡 PowerPivot 系统服务使用来选择负载平衡的初始请求的特定 PowerPivot 服务应用程序的架构。 默认设置为 **“基于运行状况”**，可基于服务器状态分配请求，服务器状态根据可用内存量和处理器使用率进行度量。 或者，您可以选择 **“循环”** ，以便无论服务器是正忙还是空闲，都按相同的重复顺序分配对服务器的请求。  
  
9. 在“数据刷新”的 **“工作时间”** 中，您可以指定用于定义工作日的小时范围。 数据刷新计划可以在下班后运行，以便选取在正常工作时间中生成的事务数据。  
  
10. 在中**PowerPivot 无人参与数据刷新帐户**，可以指定一个预定义的 Secure Store Service 目标应用程序以便存储用于运行 PowerPivot 数据刷新作业的预定义的帐户。 请确保指定目标应用程序名称而不是 ID。 如果您在 SQL Server 安装程序中使用了“新服务器”选项来安装 PowerPivot for SharePoint，则会自动创建用于无人参与的数据刷新的目标应用程序。 否则，您必须手动创建目标应用程序。 有关如何配置帐户的说明，请参阅[配置 PowerPivot 无人参与的数据刷新帐户&#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)。  
  
11. 在 **“允许用户输入自定义 Windows 凭据”** 中，您可以选中或取消选中复选框以便指定计划所有者是否可以输入任意的 Windows 凭据以便运行数据刷新计划。 如果您选中此复选框，PowerPivot 服务应用程序将为每组存储凭据都创建和管理目标应用程序。 有关详细信息，请参阅[为 PowerPivot 数据刷新配置存储凭据&#40;PowerPivot for SharePoint&#41;](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。  
  
12. 在 **“最大处理历史记录长度”** 中，您可以指定保留多长时间的数据刷新处理的历史记录。 此信息显示在为使用数据刷新的每个工作簿保留的数据刷新历史记录页中。 它还出现在 PowerPivot 管理面板中。  
  
13. 在“使用情况数据收集”的 **“查询报告间隔”** 中，指定用于报告查询统计信息的时间间隔。 查询统计信息作为单个事件报告，以便将服务器到服务器的通信量降至最低。  
  
14. 在“使用情况数据历史记录”中，指定要保留多长时间的使用情况数据的历史记录。 使用情况信息将出现在 PowerPivot 管理面板中。 如果为使用情况数据历史指定太低的值，则报告不是那么有效。  
  
15. 在“使用情况数据收集”的各查询响应阈值中，指定确定一个类别从哪里结束、另一个类别从哪里开始的上限。 这些类别建立对查询行为进行度量的基准。 您可以使用这些类别监视系统的查询响应时间中的趋势。 此信息将出现在 PowerPivot 管理面板中。  
  
16. 单击 **“确定”** 保存所做的更改。  
  
     对加载超时或分配方法的更改只应用于新的传入请求。 已在进行中的请求将受到接收请求时有效的值的影响。  
  
##  <a name="AssignGSA"></a> 将分配到 Web 应用程序的 PowerPivot 服务应用程序  
 在您配置 PowerPivot 服务应用程序后，可以通过将其添加到 Web 应用程序的服务应用程序连接列表，将其分配给该 Web 应用程序。 完成这项工作的方法有两种：  
  
-   将它添加到“默认”  连接组。 “默认连接组”  是可用于引用它的任何 Web 应用程序的服务应用程序连接的集合。 您必须将 PowerPivot 服务应用程序添加到此列表。  
  
-   为特定 Web 应用程序创建“自定义”  连接列表。 如果您创建了多个 PowerPivot 服务应用程序，则可以通过在自定义列表中选择它来选择要使用的应用程序。  
  
 默认的连接组将接受相同类型的多个服务应用程序。 但应注意，向此列表添加多个 PowerPivot 服务应用程序不是支持的配置。  
  
1.  在“管理中心”的 **“应用程序管理”** 中，单击 **“管理 Web 应用程序”**。  
  
2.  选择要为其分配连接的应用程序（例如 SharePoint -80）。  
  
3.  单击 **“服务连接”**。  
  
4.  在“编辑以下关联组”中，选择“默认值”或“[自定义]”。  
  
5.  对于“[自定义]”，选中要使用的每个服务应用程序连接旁边的复选框。 如果有多个 PowerPivot 服务应用程序 (由类型设置为指示`PowerPivot Service Application Proxy`)，确保仅选择一个。  
  
6.  单击“确定” 。  
  
##  <a name="EditGSA"></a> 编辑服务应用程序属性  
 使用下面的说明可重新打开指定服务应用程序名称、应用程序池、数据库设置和服务关联的属性页。  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  选择但不要单击 PowerPivot 服务应用程序。 您可以单击类型名称以便选择整行。  
  
3.  在功能区上单击 **“属性”** 。  
  
## <a name="see-also"></a>请参阅  
 [在管理中心中管理和配置 PowerPivot 服务器](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
