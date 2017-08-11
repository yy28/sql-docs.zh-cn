---
title: "解决 Excel 2003 行限制 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8533cd39c8a3d5efde78fee3e045eb744d562a97
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="work-around-the-excel-2003-row-limitation"></a>Work Around the Excel 2003 Row Limitation
  本主题介绍在将分页报表导出到 Excel 时，如何避开 Excel 2003 的行限制。 本解决方法适用于只包含表的报表。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 (.xls) 呈现扩展插件不推荐使用。 有关详细信息，请参阅 [SQL Server 2016 的 SQL Server Reporting Services 中不推荐使用的功能](../../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)。  
  
 Excel 2003 每个工作表最多支持 65,536 行。 您可通过在特定行数后强制添加一个显式的分页符来避开此限制。 Excel 呈现器会为每个显式分页符创建一个新的工作表。  
  
### <a name="to-create-an-explicit-page-break"></a>创建显式分页符  
  
1.  在 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 门户中打开报表。  
  
2.  右键单击表中的“数据”行，然后单击“添加组” > “父组”，以添加外部表组。  
  
     ![选择的父组](../../reporting-services/report-builder/media/datarow-selectparentgroup.png "选择父组")  
  
3.  在 **“分组依据”** 表达式框中输入下面的公式，然后单击 **“确定”** 添加父组。  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     此公式会为数据集中的每个组（65000 行为一组）分配一个编号。 如果为组定义了分页符，则此表达式会每隔 65000 行插入一个分页符。  
  
     添加外部表组会向报表添加一个组列。  
  
4.  删除组列：右键单击列标题，单击“删除列”，选择“仅删除列”，然后单击“确定”。  
  
     ![删除组列](../../reporting-services/report-builder/media/groupcolumn-delete-updated.png "删除组列")  
  
5.  右键单击 **“行组”** 部分中的 **“组 1”** ，然后单击 **“组属性”**。  
  
     ![查看组属性](../../reporting-services/report-builder/media/groupproperties-updated.png "查看组属性")  
  
6.  在 **“组属性”** 对话框的 **“排序”** 页面上，选择默认排序选项，然后单击 **“删除”**。  
  
     ![删除默认排序](../../reporting-services/report-builder/media/groupproperties-sorting-updated.png "删除默认排序")  
  
7.  在 **“分页符”** 页面上，单击 **“在组的各实例之间”** ，然后单击 **“确定”**。  
  
     ![设置分页符](../../reporting-services/report-builder/media/groupproperties-pagebreaks-updated.png "设置分页符")  
  
8.  保存报表。 在将其导出至 Excel 时，其会导出成多个工作表，且每个工作表最多包含 65000 行。  
  
  
