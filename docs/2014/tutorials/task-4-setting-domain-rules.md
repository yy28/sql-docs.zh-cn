---
title: 任务 4： 设置域规则 |Microsoft 文档
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 89e0027b3bf1748fb68a8b6922c45572a7b41bb7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025356"
---
# <a name="task-4-setting-domain-rules"></a>任务 4：设置域规则
  在此任务中，你创建的规则**联系人电子邮件**域验证的电子邮件地址如果结尾**@adventure-works.com**。 请参阅[创建域规则](http://msdn.microsoft.com/library/hh510397.aspx)页上的更多详细信息的主题。  
  
1.  单击**联系人电子邮件**中**域列表**。  
  
2.  切换到**域规则**右窗格中的选项卡。  
  
     ![添加一个新的域规则工具栏按钮](../../2014/tutorials/media/et-settingdomainrules-01.jpg "添加一个新的域规则工具栏按钮")  
  
3.  在右窗格中，单击**添加新的域规则**工具栏上的按钮 （请参阅映像） 添加规则。  
  
4.  类型**电子邮件验证**为**规则名称**按**ENTER**。 **Active**默认情况下应选中复选框。 此控件允许您临时停用某个规则。  
  
5.  在**生成规则**窗格中，单击**向下箭头**，然后选择**值结尾**。  
  
6.  类型**@adventure-works.com**文本框中，然后按**选项卡**。 您可以通过单击添加更多条件**向所选子句添加新的条件**中的工具栏按钮**生成规则**窗格。  
  
     ![电子邮件验证规则](../../2014/tutorials/media/et-settingdomainrules-02.jpg "电子邮件验证规则")  
  
7.  单击**对测试数据运行所选的域规则**在右侧窗格中测试规则所依据示例数据中的工具栏按钮。  
  
     ![对测试数据工具栏按钮运行域规则](../../2014/tutorials/media/et-settingdomainrules-03.jpg "对测试数据工具栏按钮运行域规则")  
  
8.  在**测试域规则**对话框中，单击**添加新的测试字词为域规则**工具栏上的按钮。  
  
     ![测试域规则对话框](../../2014/tutorials/media/et-settingdomainrules-04.jpg "测试域规则对话框")  
  
9. 类型**frank7@adventure-works.com** （有效的值） 中**联系人电子邮件**列。  
  
10. 重复前面的两个步骤以添加**joe2@adventure-work.com** (不带值无效的)。  
  
11. 单击最后一个按钮 (**对所有字词测试域规则**) 在工具栏上，若要测试根据规则的输入的数据。  
  
     ![测试域规则上所有条款工具栏按钮](../../2014/tutorials/media/et-settingdomainrules-05.jpg "测试域规则上所有条款工具栏按钮")  
  
12. 请注意第一个条目显示为有效项，而第二个条目显示为无效项。  
  
     ![测试域规则结果](../../2014/tutorials/media/et-settingdomainrules-06.jpg "测试域规则结果")  
  
13. 单击**关闭**关闭**测试域规则**对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 5：设置基于字词的关系](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  