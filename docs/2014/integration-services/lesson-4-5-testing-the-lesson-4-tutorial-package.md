---
title: 步骤 5：测试第 4 课教程包 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fab91a2df7d0401e8301589b1dd0d21027e579c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62891282"
---
# <a name="step-5-testing-the-lesson-4-tutorial-package"></a>步骤 5：测试第 4 课教程包
  在运行时，损坏的文件 Currency_BAD.txt 将无法在 Currency Key 查找转换中生成匹配。 由于 Currency Key 查找的错误输出现在已配置为将失败的行重定向到新的失败的行目标，因此该组件不会失败，并且包会成功地运行。 所有失败的错误行都将写入 ErrorOutput.txt。  
  
 在此任务中，您将通过运行该包对已修改的错误输出配置进行测试。 包成功执行后，您将查看 ErrorOutput.txt 文件的内容。  
  
> [!NOTE]  
>  如果不需要在 ErrorOutput.txt 文件中积累错误行，则应在包的运行间隔手动删除文件内容。  
  
## <a name="checking-the-package-layout"></a>检查包布局  
 测试包之前，应当确保第 4 课包中的控制流和数据流包含下列关系图中显示的对象。 控制流应与第 2 到第 4 课中的控制流相同。  
  
 **控制流**  
  
 ![包中的控制流](../../2014/tutorials/media/task4lesson2control.gif "包中的控制流")  
  
 **数据流**  
  
 ![包中的数据流](../../2014/tutorials/media/task5lesson5data.gif "包中的数据流")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>运行第 4 课教程包  
  
1.  在 **“调试”** 菜单中，单击 **“启动调试”** 。  
  
2.  当包运行完毕后，在 **“调试”** 菜单中，单击 **“停止调试”** 。  
  
### <a name="to-verify-the-contents-of-the-erroroutputtxt-file"></a>验证 ErrorOutput.txt 文件的内容  
  
-   在记事本或任何其他文本编辑器中，打开 ErrorOutput.txt 文件。 默认的列顺序为：AverageRate、CurrencyID、CurrencyDate、EndOfDateRate、ErrorCode、ErrorColumn、ErrorDescription。  
  
     请注意，文件中的所有行都包含不匹配的 CurrencyID 值 BAD、ErrorCode 值 -1071607778、ErrorColumn 值 0 以及 ErrorDescription 值“在查找期间行没有生成任何匹配项”。 由于此错误并不是列所特有的，所以 ErrorColumn 的值设置为 0。 它是已失败的查找操作。 .  
  
  
