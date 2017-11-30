---
title: "Power Pivot 连接类型 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a104c3c7-f118-4d02-9a0f-6859f1469d11
caps.latest.revision: "9"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7a8fe1f1b6dd44f468095502b924c432032cf11d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="power-pivot-connection-type-ssrs"></a>Power Pivot 连接类型 (SSRS)
  可以使用 SQL Server Analysis Services 数据处理扩展插件从在 SharePoint [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库中发布的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿检索数据。  
  
 使用本主题中的信息来生成一个数据源。 有关分步说明，请参阅 [添加和验证数据连接（报表生成器和 SSRS）](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
## <a name="prerequisites"></a>先决条件  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源必须发布在 SharePoint 站点上的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库中。  
  
 为了支持从报表生成器到 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿的连接，工作站计算机上必须具有 SQL Server 2008 R2 ADOMD.NET。 此客户端库与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 一起安装，但如果你在使用不具有此应用程序的计算机，则必须从 [SQL Server 2008 R2 功能包](http://go.microsoft.com/fwlink/?LinkId=192565)下载和安装 ADOMD.NET。  
  
## <a name="data-source-type"></a>数据源类型  
 使用报表数据源类型： **Microsoft SQL Server Analysis Services**。  
  
## <a name="connection-string"></a>连接字符串  
 连接字符串是指向 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库或其他库中在 SharePoint 上发布的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿的 URL，例如，`http://contoso-srv/subsite/PowerPivotLibrary/ContosoSales.xlsx`。  
  
## <a name="credentials"></a>凭据  
 指定访问 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿和 SharePoint 站点所需的凭据，例如 Windows 身份验证（集成安全性）。 有关详细信息，请参阅[数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)或[在报表生成器中指定凭据](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
## <a name="queries"></a>查询  
 在连接到 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源之后，使用 MDX 图形查询，通过从基础数据结构中浏览并进行选择来生成查询。 生成查询后，运行该查询在“结果”窗格中查看示例数据。  
  
 查询设计器将对查询进行分析，以确定数据集字段。 您也可以在 **“报表数据”** 窗格中手动编辑数据集字段集合。 有关详细信息，请参阅[在“报表数据”窗格中添加、编辑和刷新字段（报表生成器和 SSRS）](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)。  
  
## <a name="filters"></a>筛选器  
 在“筛选器”窗格中，指定要在查询结果中排除或包含的维度和成员。  
  
## <a name="parameters"></a>Parameters  
 在“筛选器”窗格中，针对某个筛选器选择 **“参数”** 选项，以便自动使用与所选筛选器对应的可用值创建报表参数。  
  
## <a name="remarks"></a>注释  
 如果从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿打开报表生成器，则不会在报表中重新创建 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿中的数据透视表、数据透视图、切片器以及其他布局和分析功能。 而是生成一个空报表，其中包含一个预配置的数据源，该数据源指向 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿中的数据。 基于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿设计报表可能很费时费力，具体取决于要在报表中重新创建的切片器、筛选器以及表或图表的数量。 一个更好的方法是独立于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 设计构思你要包含在报表中的数据的显示格式。  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿中的数据经过高度压缩；而从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿中为报表检索的数据未经压缩。 使用查询设计器可指定筛选器和参数，以便将数据限制为仅是报表中所需的数据。  
  
 与连接到 Analysis Services 多维数据集不同， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 模型没有层次结构。 为了向工作簿中的相关切片器提供类似功能，您必须在报表中创建级联参数。 有关详细信息，请参阅 [向报表添加级联参数（报表生成器和 SSRS）](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)中所创建的移动报表中使用。  
  
 在某些情况下，可能需要调整表达式，以容纳 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 模型中的基础数据值。 您可能需要修改表达式，以便将数据转换为正确的数据类型，或者添加或删除聚合函数。 例如，要将数据类型从 String 转换为 Integer，请使用 `=CInt`。 请始终在发布报表之前，验证报表从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 模型中的数据显示预期的值。  
  
 仅当满足以下条件时，才能生成 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库中报表的预览图像：  
  
-   提供数据的报表和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿必须在同一 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库中一起存储。  
  
-   报表仅包含来自 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services MDX 查询设计器用户界面（报表生成器）](http://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26)   
 [表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
