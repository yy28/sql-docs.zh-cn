---
title: 步骤 8：为第 1 课包添加批注并设置格式 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f830393b516ac583a6c0ae72332bef8ac8177714
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65722841"
---
# <a name="lesson-1-8-annotate-and-format-the-lesson-1-package"></a>第 1-8 课：为第 1 课包添加批注并设置格式 

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



完成第 1 课包的配置后，现在即可整理包布局。 如果控件和数据流布局中的形状大小不同，或者布局不均匀，则可能更难理解包。  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 提供了轻松设置包布局格式的工具。 格式设置功能包括使形状大小统一、对齐各个形状、以及更改形状之间的水平间距和垂直间距。  
  
另一种增进对包功能的了解的方式是添加描述包功能的批注。  
  
在本任务中，将使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 中的格式设置功能来改进数据流的布局以及添加批注。  
  
## <a name="format-the-layout-of-the-data-flow"></a>设置数据流的布局格式  
  
1.  如果尚未打开第 1 课包，请在“解决方案资源管理器”中双击“Lesson 1.dtsx”。  
  
2.  单击“数据流”选项卡。  
  
3.  要同时全选数据流组件，请使用“编辑” > “全选”。
  
4.  在“格式”菜单中，依次选择“设为相同大小”、“两者”。  
  
5.  选定数据流对象后，在“格式”菜单中，依次选择“对齐”、“居中”。  

6.  选定数据流对象后，在“格式”菜单中，依次选择“垂直间距”、“设为相等”。  
  
## <a name="add-an-annotation-to-the-data-flow"></a>向数据流添加批注  
  
1.  右键单击数据流设计图面背景的任意位置，然后选择“添加批注”。  
  
2.  在批注框中输入或粘贴以下文本。  
  
        The data flow extracts data from a file, looks up values in the CurrencyKey column in the DimCurrency table and the DateKey column in the DimDate table, and writes the data to the NewFactCurrencyRate table.
  
    要在批注框中使文本换行，请将光标置于要开始新行的位置，然后按 Enter。  
  
    如果不向批注框添加文本，单击批注框外部即可取消该框。  
  
## <a name="go-to-next-task"></a>转到下一个任务
[步骤 9：测试第 1 课包](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
  
