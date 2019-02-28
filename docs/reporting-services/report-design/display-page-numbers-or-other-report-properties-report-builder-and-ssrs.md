---
title: 显示页码或其他报表属性（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: c7d95245-4709-4d04-acb4-59bf71e60d97
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 576d2fc5ba8ea023e69fe9b6136a676b188366e4
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56296795"
---
# <a name="display-page-numbers-or-other-report-properties-report-builder-and-ssrs"></a>显示页码或其他报表属性（报表生成器和 SSRS）
  可以方便地向报表的页眉或页脚添加页码、报表标题、文件名和其他报表属性。 这些属性在“报表数据”窗格的“内置字段”文件夹中存储为字段：  
  
-   执行时间  
  
-   页码  
  
-   报表文件夹  
  
-   报表名称  
  
-   报表服务器 URL  
  
-   全部页  
  
-   用户 ID  
  
-   “报表”  
  
 对于页码，您可能希望在数字前添加单词“Page”。 也可能希望显示总页数。  
  
> [!NOTE]  
>  将总页数添加到页脚在运行或预览报表时可能会降低性能。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-page-number-or-other-report-properties"></a>添加页码或其他报表属性  
  
1.  在“报表数据”窗格中，展开“内置字段”文件夹。  
  
    > [!NOTE]  
    >  如果看不到“报表数据”窗格，请在“视图”选项卡上选中“报表数据”。  
  
2.  将 **“页码”** 字段从“报表数据”窗格拖动到报表表头和表尾。  
  
    > [!NOTE]  
    >  页脚将自动添加到报表。 若要添加页眉，请在 **“插入”** 选项卡上，单击 **“页眉”**，然后单击 **“添加页眉”**。  
    >   
    >  将添加一个包含简单表达式 [&PageNumber] 的文本框。  
  
### <a name="to-add-the-word-page-before-the-page-number"></a>在页码前添加单词 "Page"  
  
1.  右键单击包含 [&PageNumber] 的文本框，然后单击“表达式”。  
  
     “为以下项设置表达式: Value”文本框包含表达式 =Globals!PageNumber。  
  
2.  将光标放在 = 号后，然后键入 "Page " &。  
  
     该表达式现在变为 ="Page "&Globals!PageNumber  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-total-number-of-pages-after-the-page-number"></a>在页码后面添加总页数  
  
1.  右键单击包含表达式的文本框，然后单击 **“表达式”**。  
  
2.  在表达式的末尾键入 &" of "&。  
  
3.  在“类别”窗格中，展开“内置字段”，然后双击 TotalPages。  
  
     该表达式现在变为 ="Page "&Globals!PageNumber &" of "&Globals!TotalPages  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [页眉和页脚（报表生成器和 SSRS）](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [设置文本框中文本的格式（报表生成器和 SSRS）](../../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
  
