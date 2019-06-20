---
title: 创建到 PowerPivot 工作簿的 BI 语义模型连接 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b2e3f97f-18a8-42b6-9030-b4f818afc3b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f525c45e71c290d3eaab410c0fa0fa62d1e9a61d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071636"
---
# <a name="create-a-bi-semantic-model-connection-to-a-powerpivot-workbook"></a>创建与 PowerPivot 工作簿的 BI 语义模型连接
  使用本主题中的信息可设置一个 BI 语义模型连接，该连接重定向到同一个场中的 PowerPivot 工作簿。  
  
 在您创建了 BI 语义模型连接并且配置了 SharePoint 权限后，可以将其用作 Excel 或 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报表的数据源。  
  
 本主题包含以下各节。 按给出的顺序执行每个任务。  
  
 [检查必备条件](#bkmk_prereq)  
  
 [创建连接](#bkmk_create)  
  
 [配置针对 BI 语义模型连接的 SharePoint 的权限](#bkmk_permissions)  
  
 [配置针对工作簿的 SharePoint 权限](#bkmk_userdb)  
  
 [后续步骤](#bkmk_next)  
  
##  <a name="bkmk_prereq"></a> 检查必备条件  
 您必须具有“参与讨论”权限或更高权限以创建 BI 语义模型连接文件。  
  
 您必须具有支持 BI 语义模型连接内容类型的库。 有关详细信息，请参阅[将 BI 语义模型连接内容类型添加到库&#40;PowerPivot for SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md)。  
  
 您必须知道为其设置 BI 语义模型连接的 PowerPivot 工作簿的 URL (例如， http://adventure-works/shared documents/myworkbook.xlsx)。 工作簿必须位于同一场中。  
  
 参与连接序列的所有计算机和用户都必须处于同一个域或可信域（双向信任）中。  
  
##  <a name="bkmk_create"></a> 创建连接  
  
1.  在将包含 BI 语义模型连接的库中，单击 SharePoint 功能区上的 **“文档”** 。 单击“新建文档”上的向下箭头，然后选择 **“BISM 连接文件”** 以便打开“新建 BI 语义模型连接”页。  
  
     ![在 SharePoint 库中的新文档子菜单](../media/ssas-bismconnection-new.gif "SharePoint 库中的新建文档子菜单")  
  
2.  设置**服务器**属性设置为 PowerPivot 工作簿的 SharePoint URL (例如，  **http://mysharepoint/shared documents/Myworkbook.xlsx**。 在 PowerPivot for SharePoint 部署中，数据可从场中的任何服务器上加载。 因此，与 PowerPivot 数据的数据源连接仅指定指向工作簿的路径。 PowerPivot 系统服务将确定哪一服务器将加载数据。  
  
     不要使用**数据库**属性; 指定的 PowerPivot 工作簿的位置时不使用。  
  
     页面的外观应该如下图所示。  
  
     ![显示 URL 到工作簿的 BISM 连接页](../media/ssas-bismconnection-ppvtds.gif "到工作簿中显示 URL 的 BISM 连接页")  
  
     或者，如果您具有针对工作簿的 SharePoint 权限，则要执行一个附加的验证步骤，以便确保该位置有效。 如果您没有对数据的访问权限，则会向您提供一个无需验证响应即保存 BI 语义模型连接的选项。  
  
##  <a name="bkmk_permissions"></a> 配置针对 BI 语义模型连接的 SharePoint 的权限  
 为了能够使用 BI 语义模型连接作为 Excel 工作簿或 Reporting Services 报表的数据源，需要针对 SharePoint 库中 BI 语义模型连接项的 **“读取”** 权限。 该“读取”权限级别包括 **“打开项”** 权限，该权限支持将 BI 语义模型连接信息下载到 Excel 桌面应用程序。  
  
 有几种方法可在 SharePoint 中授予权限。 下面的说明解释如何新建一个名为 **BISM Users** 的具有“读取”  权限级别的组。  
  
 您必须是网站所有者才能更改权限。  
  
1.  在“网站操作”中，单击 **“网站权限”** 。  
  
2.  单击“创建组”  并将新组命名为 **BISM Users**。  
  
3.  选择 **“读取”** 权限级别，然后单击 **“创建”** 。  
  
4.  在“人员和组”中选择 **BISM Users** 。  
  
5.  指向“新建”，单击 **“添加用户”** ，然后添加用户或组帐户。  
  
     此时，这些用户和组将拥有对整个网站的“读取”权限，包括从网站级别继承权限的所有库和列表。 如果这些权限太高，则可以选择从特定的库、列表或项中删除此组。  
  
 若要选择性地删除项目级别的权限，请执行以下操作：  
  
1.  在库中选择一个文档。 单击右下箭头，然后单击 **“管理权限”** 。  
  
2.  默认情况下，项会继承权限。 若要更改此库中的单个文档的权限，请单击 **“停止继承权限”** 。  
  
3.  选中  “BISM 用户”旁的复选框。  
  
4.  单击 **“删除用户权限”** 。  
  
##  <a name="bkmk_userdb"></a> 配置针对工作簿的 SharePoint 权限  
 如果您在一个 Excel 工作簿内使用某一 PowerPivot 数据库，则针对该 Excel 工作簿的 SharePoint 权限将确定通过 BI 语义模型连接进行的数据访问。 为了将工作簿用作外部数据源，访问该工作簿的所有用户都必须对工作簿具有读取权限。  
  
 如果你使用了前一部分中的说明创建了 **BISM Users** 组，则 **BISM Users** 组成员的用户和组帐户将拥有该工作簿以及 BI 语义模型连接文件的足够权限，并且假定该工作簿使用继承的权限。  
  
##  <a name="bkmk_next"></a> 后续步骤  
 创建了 BI 语义模型连接并且确保其安全后，可以将该连接指定为数据源。 有关详细信息，请参阅 [在 Excel 或 Reporting Services 中使用 BI 语义模型连接](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [PowerPivot BI 语义模型连接&#40;.bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)   
 [在 Excel 或 Reporting Services 中使用 BI 语义模型连接](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)   
 [创建与表格模型数据库的 BI 语义模型连接](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
  
