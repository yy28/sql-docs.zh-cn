---
title: 任务4：设置域规则 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0104fe6b64ff2ecc1a37bb1da9691e34d7913f21
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061092"
---
# <a name="task-4-setting-domain-rules"></a>任务 4：设置域规则
  在此任务中，你将为**联系人电子邮件**域创建一个规则，以验证该电子邮件地址是否以** \@ adventure-works.com**结尾。 有关详细信息，请参阅[创建域规则](https://msdn.microsoft.com/library/hh510397.aspx)主题。  
  
1.  单击 "**域列表**" 中的 "**联系人电子邮件**"。  
  
2.  切换到右窗格中的 "**域规则**" 选项卡。  
  
     ![“添加新的域规则”工具栏按钮](../../2014/tutorials/media/et-settingdomainrules-01.jpg "“添加新的域规则”工具栏按钮")  
  
3.  在右侧窗格中，单击工具栏上的 "**添加新的域规则**" 按钮（请参阅图像）以添加规则。  
  
4.  为 "**规则名称**" 键入**电子邮件验证**，然后按**enter**。 默认情况下，应选中 "**活动**" 复选框。 此控件允许您临时停用某个规则。  
  
5.  在 "**生成规则**" 窗格中，单击**向下箭头**，然后选择 "**值结束于**"。  
  
6.  在文本框中键入** \@ adventure-works.com** ，然后按**tab**。 您可以通过在 "**生成规则**" 窗格中单击 **"向选定子句添加新条件"** 工具栏按钮来添加更多条件。  
  
     ![电子邮件验证规则](../../2014/tutorials/media/et-settingdomainrules-02.jpg "电子邮件验证规则")  
  
7.  单击右窗格中工具栏上的 "**对测试数据运行所选域规则**" 按钮，针对示例数据测试规则。  
  
     ![“对测试数据运行域规则”工具栏按钮](../../2014/tutorials/media/et-settingdomainrules-03.jpg "“对测试数据运行域规则”工具栏按钮")  
  
8.  在 "**测试域规则**" 对话框中，单击工具栏上**的 "为域规则添加新的测试字词"** 。  
  
     ![“测试域规则”对话框](../../2014/tutorials/media/et-settingdomainrules-04.jpg "“测试域规则”对话框")  
  
9. 在 "**联系人电子邮件**" 列中键入**frank7 \@ adventure-works.com** （有效的值）。  
  
10. 重复上述两个步骤，添加**joe2 \@ adventure-work.com** （不包含 "s" 的无效值）。  
  
11. 单击工具栏上的 "最后一个" 按钮（"**测试域规则**"），根据规则测试输入数据。  
  
     ![“针对所有字词测试域规则”工具栏按钮](../../2014/tutorials/media/et-settingdomainrules-05.jpg "“针对所有字词测试域规则”工具栏按钮")  
  
12. 请注意第一个条目显示为有效项，而第二个条目显示为无效项。  
  
     ![测试域规则结果](../../2014/tutorials/media/et-settingdomainrules-06.jpg "测试域规则结果")  
  
13. 单击 "**关闭**" 以关闭 "**测试域规则**" 对话框。  
  
## <a name="next-step"></a>后续步骤  
 [任务 5：设置基于字词的关系](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  
