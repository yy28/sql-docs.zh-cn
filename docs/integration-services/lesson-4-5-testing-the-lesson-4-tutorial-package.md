---
title: 步骤 5：测试第 4 课教程包 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2725731d216b651d310b204f4cdf6b19612ae435
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055812"
---
# <a name="lesson-4-5-test-the-lesson-4-package"></a>第 4-5 课：测试第 4 课包

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在运行时，损坏的文件“Currency_BAD.txt”无法在 Currency Key 查找转换中生成匹配项。 由于将 Currency Key 查找的错误输出配置为将失败的行重定向到新的失败的行目标，因此该组件不会失败，并且包会成功地运行。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 将所有失败的行写入“ErrorOutput.txt”。  
  
在此任务中，通过运行该包对已修改的错误输出配置进行测试。 包成功执行后，可查看“ErrorOutput.txt”文件的内容。  
  
> [!NOTE]  
> 如果不需要在“ErrorOutput.txt”文件中积累错误行，请在包的运行间隔手动删除文件内容。  
  
## <a name="check-the-package-layout"></a>检查包布局  
在测试包之前，请验证第 4 课包中的控制流和数据流是否与下图类似： 
  
**控制流**  
  
![包中的控制流](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**数据流**  
  
![包中的数据流](../integration-services/media/task5lesson5data.gif "Data flow in package")  
  
## <a name="run-the-lesson-4-tutorial-package"></a>运行第 4 课教程包  
  
1.  在“调试”菜单中，选择“启动调试”。  
  
2.  当包运行完毕后，在“调试”菜单中，选择“停止调试”。  
  
## <a name="view-the-contents-of-the-erroroutputtxt-file"></a>查看 ErrorOutput.txt 文件的内容  
  
在记事本或其他文本编辑器中，打开“ErrorOutput.txt”文件。 默认的列顺序为：AverageRate、CurrencyID、CurrencyDate、EndOfDateRate、ErrorCode、ErrorColumn、ErrorDescription。  
 
文件中的所有行都包含不匹配的 CurrencyID 值“BAD”、ErrorCode 值 - 1071607778、ErrorColumn 值 0 以及 ErrorDescription 值“在查找期间行没有生成任何匹配项”。 ErrorColumn 的值为 0，因为错误不是特定于列的，而是查找操作失败。
  
  
## <a name="next-lesson"></a>下一课
[第 5 课：添加包部署模型的 SSIS 包配置](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
