---
title: 避开 Excel 2003 行限制 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3a01ffa473a45a17cfab39fd0ab8cfc86d5cb022
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33019424"
---
# <a name="work-around-the-excel-2003-row-limitation"></a>Work Around the Excel 2003 Row Limitation
  本主题介绍在将分页报表导出到 Excel 时，如何避开 Excel 2003 的行限制。 本解决方法适用于只包含表的报表。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 (.xls) 呈现扩展插件不推荐使用。 有关详细信息，请参阅 [SQL Server 2016 的 SQL Server Reporting Services 中不推荐使用的功能](../../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)。  
  
 Excel 2003 每个工作表最多支持 65,536 行。 您可通过在特定行数后强制添加一个显式的分页符来避开此限制。 Excel 呈现器会为每个显式分页符创建一个新的工作表。  
  
### <a name="to-create-an-explicit-page-break"></a>创建显式分页符  
  
1.  在 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 门户中打开报表。  
  
2.  右键单击表中的“数据”行，然后单击“添加组” > “父组”，以添加外部表组。  
  
     ![选择父组](../../reporting-services/report-builder/media/datarow-selectparentgroup.png "Select the Parent Group")  
  
3.  在 **“分组依据”** 表达式框中输入下面的公式，然后单击 **“确定”** 添加父组。  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     此公式会为数据集中的每个组（65000 行为一组）分配一个编号。 如果为组定义了分页符，则此表达式会每隔 65000 行插入一个分页符。  
  
     添加外部表组会向报表添加一个组列。  
  
4.  删除组列：右键单击列标题，单击“删除列”，选择“仅删除列”，然后单击“确定”。  
  
     ![删除组列](../../reporting-services/report-builder/media/groupcolumn-delete-updated.png "Delete a group column")  
  
5.  右键单击 **“行组”** 部分中的 **“组 1”** ，然后单击 **“组属性”**。  
  
     ![查看组属性](../../reporting-services/report-builder/media/groupproperties-updated.png "View group properties")  
  
6.  在 **“组属性”** 对话框的 **“排序”** 页面上，选择默认排序选项，然后单击 **“删除”**。  
  
     ![删除默认排序](../../reporting-services/report-builder/media/groupproperties-sorting-updated.png "Delete default sorting")  
  
7.  在 **“分页符”** 页面上，单击 **“在组的各实例之间”** ，然后单击 **“确定”**。  
  
     ![设置分页符](../../reporting-services/report-builder/media/groupproperties-pagebreaks-updated.png "Set page breaks")  
  
8.  保存报表。 在将其导出至 Excel 时，其会导出成多个工作表，且每个工作表最多包含 65000 行。  
  
  
