---
title: 任务 4：管理和查看报表 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ecc3ba7e-fecf-478f-8825-6e4764b00e99
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2df7517a8043269efe40d21b112100edaf9e847f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489456"
---
# <a name="task-4-manaing-and-viewing-results"></a>任务 4：管理和查看报表
  在该任务中，您查看计算机辅助清理的结果，还对供应商数据执行交互式清理。 请参阅[交互式清理阶段](https://msdn.microsoft.com/library/hh213061.aspx#Interactive)的更多详细信息。  
  
1.  选择**Contact Email**从域列表的域。  
  
2.  切换到**无效**右窗格中的选项卡。 请注意，两个电子邮件地址缺少字符的结尾。 这些被认为是无效的要求所有电子邮件地址结尾的域规则的两个电子邮件 **@adventure-works.com** (使用的)。 在清理时，DQS 使用此域规则来确定电子邮件是否有效。 此选项卡显示在知识库中被标记为无效的域值或不符合域规则要求的值。 在这种情况下，这些值不符合域规则的要求（电子邮件验证）。  
  
3.  在中 **更正为** 列中，键入正确的电子邮件地址结尾 **@adventure-works.com** (使用的)。  
  
     ![从电子邮件验证规则的更正](../../2014/tutorials/media/et-managingandviewingresults-01.jpg "从电子邮件验证规则的更正")  
  
4.  单击**批准**这两个要批准这两个更改的记录。 当您批准后时，记录将移至 **已更正** 选项卡。而不是单独批准每个项，可使用一次的所有更改进行都审批 **都批准所有字词** 工具栏按钮。  
  
5.  切换到 **新建** 右窗格中的选项卡。 此选项卡上的值是 DQS 在知识库中尚未具有足够的信息来确定其是否正确的值。 因此，它无法更改域值，也无法建议对域值所做的更改。  
  
6.  检查这些值以确认所有电子邮件结尾 **@adventure-works.com** 然后单击 **批准所有字词** 工具栏上。 此选项卡中的已批准的值将移到 **更正** 选项卡。  
  
7.  选择**国家/地区**从域列表的域。  
  
8.  切换到**已更正**选项卡上，在右窗格中，可以看到**United State**值自动更正为**美国**使用的结尾。 此规则不是为定义的规则**国家/地区**域，但 DQS 以**83%** 确信正确的值是**美国**。 **批准**按钮自动选择所有**已更正**项。 您可以覆盖此行为并拒绝更改。  
  
9. 请注意， **USA**更正为**美国**因为它们是同义词并**美国**是前导 （首选） 值。  
  
     ![基于同义词的更正](../../2014/tutorials/media/et-managingandviewingresults-02.jpg "更正根据同义词")  
  
10. 请注意，**批准**按钮已处于选中状态，针对这些更正的值。 此行为对于更正的值是默认行为。 您可以拒绝更改，当你执行此操作，值将移到**无效**选项卡。  
  
11. 选择**Supplier Name**从域列表。  
  
12. 切换到**已更正**右窗格中的选项卡。  
  
     ![更正了供应商名称](../../2014/tutorials/media/et-managingandviewingresults-03.jpg "更正了供应商名称")  
  
    1.  请注意， **A.Datum Corp.** 更正为**A.Datum Corporation**并**原因**设置为**基于字词的关系。A.datum Corporation**是 dqs 已知的域值，因为它在知识发现过程中发现。 因此，DQS 会**100%信任**此更正。  
  
    2.  请注意， **Lazy Country Storex**更正为**Lazy Country Store**，**置信度级别**设置为**100%** ，和**原因**设置为**域值**。 在知识发现过程中，设置**Lazy Country Storex**视为与错误**Lazy Country Store**作为**更正**，因此 DQS **100%确信**有关进行此项更改。  
  
    3.  DQS 不熟悉的其他值在列表中，但找到使用这些值的更正**拼写检查器**并提出了合适的更正。 DQS 是**并非 100%** 信任这些更改，但置信度高于 80%，这是进行更改，因此 DQS 建议进行这些更改的阈值级别。  
  
13. 请注意，**批准**自动启用的所有值。 您可以相应地覆盖更正后的值或拒绝更改。 默认情况下**批准**上的所有值选择按钮**已更正**选项卡。  
  
14. 切换到**新建**选项卡。  
  
15. 请注意， **Corp.** 更正为**Corporation**， **Co.** 更正为**公司**，和**Inc.** 更正为**Incorporated**。 例如， **Consolidate Inc.** 更正为**Consolidate Incorporated**并**Consolidated Co.** 更正为**Consolidated Company**，并**Frabrikam Corp.** 更正为**Fabrikam Corporation**。  你可以看到**基于字词的关系**成为了原因。 可以使用您在域管理活动中定义的基于字词的关系来针对这些更改提出建议。 您可以更改**更正为**手动此处的值。  
  
16. 滚动列表以查看**Hunxgry Coyote Store**用红色的波浪线。 右键单击它并单击**Hungy Coyote Store** （与没有 x)。 **更正为**列应自动填充了**Hungry Coyote Store**。 您也可以在“更正为”列中手动键入值。  
  
17. 单击**批准所有字词**从工具栏中。 域值**更正为**指定的值将移到**已更正**选项卡上和没有关联的新值**更正为**的值将移到**正确**选项卡。  
  
18. 选择**地址验证**从域列表的复合域。  
  
19. 在右窗格中，切换到**更正**选项卡。应会看到找到是正确的地址**Melissa 数据-地址检查**上的 DQS 服务**Azure Marketplace**。  
  
20. 切换到**已更正**选项卡。  
  
21. 请注意，**状态**记录具有**市/县**作为**Los Angeles**设置为**CA**现在。 请注意，在**原因**字段是**更正规则城市-州规则**。  
  
     ![城市-州规则更正](../../2014/tutorials/media/et-managingandviewingresults-04.jpg "城市-州规则更正")  
  
22. 请注意，**批准**已为该项目在列表中选择单选按钮。 这是上项的默认行为**已更正**选项卡。  
  
23. 切换到**建议**选项卡。查看建议的更改**Melissa 数据-地址检查**服务。  
  
24. **单击批准所有字词**工具栏按钮，然后都单击**确定**上**确认**消息框。  
  
     ![批准所有字词工具栏按钮](../../2014/tutorials/media/et-managingandviewingresults-05.jpg "都批准所有字词工具栏按钮")  
  
25. 单击**下一步**若要切换到**导出**页。  
  
## <a name="next-step"></a>下一步  
 [任务 5：将清理结果保存到 Excel 文件导出](../../2014/tutorials/task-5-exporting-cleansing-results-to-an-excel-file.md)  
  
  
