---
title: 显示页码或其他报表属性 （报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c7d95245-4709-4d04-acb4-59bf71e60d97
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0aa360b52f6928db53a473712c38bbfc2d05de78
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63135483"
---
# <a name="display-page-numbers-or-other-report-properties-report-builder-and-ssrs"></a>显示页码或其他报表属性 （报表生成器和 SSRS）
  它很容易将页码、 报表标题、 文件名和其他报表属性添加到页眉或页脚的报表。 这些属性存储为报表数据窗格中的内置字段文件夹中的字段：  
  
-   执行时间  
  
-   页码  
  
-   报表文件夹  
  
-   报告名称  
  
-   报表服务器 URL  
  
-   总页数  
  
-   User ID  
  
-   语言  
  
 页码，您可能想要添加数字前的单词"Page"。 您可能想要显示的页总数。  
  
> [!NOTE]  
>  在运行或预览报表时，将总页数添加到页脚中可能会降低性能。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-page-number-or-other-report-properties"></a>若要添加页码或其他报表属性  
  
1.  在报表数据窗格中，展开内置字段文件夹。  
  
    > [!NOTE]  
    >  如果您看不到报表数据窗格中，在视图选项卡上，检查**报表数据**。  
  
2.  拖动**页码**字段从报表数据窗格向报表页眉或页脚。  
  
    > [!NOTE]  
    >  页脚将自动添加到报表。 若要添加页眉，在**插入**选项卡上，单击**标头**，然后单击**添加标头**。  
    >   
    >  添加包含简单表达式 [& PageNumber] 的文本框。  
  
### <a name="to-add-the-word-page-before-the-page-number"></a>若要添加单词"Page"页码前  
  
1.  右键单击包含 [&] 的文本框 PageNumber，然后单击**表达式**。  
  
     **设置表达式：值**文本框包含表达式 = Globals ！PageNumber。  
  
2.  将光标放在 = 号和类型之后`"Page " &`。  
  
     现在 = 表达式"页"& Globals ！PageNumber  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-total-number-of-pages-after-the-page-number"></a>页码后面添加总页数  
  
1.  右键单击包含表达式和单击文本框**表达式**。  
  
2.  类型 **（& a)"的"&** 表达式的末尾。  
  
3.  在类别窗格中，展开**内置字段**，然后双击**TotalPages**。  
  
     现在 = 表达式"页"& Globals ！PageNumber &"的"& Globals ！TotalPages  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [页眉和页脚&#40;报表生成器和 SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)   
 [中的文本框中的文本格式&#40;报表生成器和 SSRS&#41;](format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
  
