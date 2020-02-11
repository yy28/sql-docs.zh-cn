---
title: 解决 Excel 行限制 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 84f01e85a0a93ef1f2a14b2b01b4180143153865
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107553"
---
# <a name="work-around-the-excel-row-limitation"></a>避开 Excel 行限制
  本主题介绍在将报表导出到 Excel 时，如何避开 Excel 2003 的行限制。 本解决方法适用于只包含表的报表。  
  
 Excel 2003 每个工作表最多支持 65,536 行。 您可通过在特定行数后强制添加一个显式的分页符来避开此限制。 Excel 呈现器会为每个显式分页符创建一个新的工作表。  
  
### <a name="to-create-an-explicit-page-break"></a>创建显式分页符  
  
1.  在 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] 或报表管理器中打开报表。  
  
2.  右键单击表中的数据行，然后单击 "**添加组** > " "**父组**" 以添加外部表组。  
  
     ![选择父组](../media/datarow-selectparentgroup.png "选择父组")  
  
3.  在 **“分组依据”** 表达式框中输入下面的公式，然后单击 **“确定”** 添加父组。  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     此公式会为数据集中的每个组（65000 行为一组）分配一个编号。 如果为组定义了分页符，则此表达式会每隔 65000 行插入一个分页符。  
  
     添加外部表组会向报表添加一个组列。  
  
4.  删除组列：右键单击列标题，单击“删除列”，选择“仅删除列”，然后单击“确定”。************  
  
     ![删除组列](../media/groupcolumn-delete-updated.png "删除组列")  
  
5.  右键单击 **“行组”** 部分中的 **“组 1”** ，然后单击 **“组属性”**。  
  
     ![查看组属性](../media/groupproperties-updated.png "查看组属性")  
  
6.  在 **“组属性”** 对话框的 **“排序”** 页面上，选择默认排序选项，然后单击 **“删除”**。  
  
     ![删除默认排序](../media/groupproperties-sorting-updated.png "删除默认排序")  
  
7.  在 **“分页符”** 页面上，单击 **“在组的各实例之间”** ，然后单击 **“确定”**。  
  
     ![设置分页符](../media/groupproperties-pagebreaks-updated.png "设置分页符")  
  
8.  保存报表。 在将其导出至 Excel 时，其会导出成多个工作表，且每个工作表最多包含 65000 行。  
  
  
