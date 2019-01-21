---
title: 步骤 2：创建损坏的文件 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d81ac7d0a5c7a42a2292bab7ca5beffa464d02d7
ms.sourcegitcommit: e2fa721b6f46c18f1825dd1b0d56c0a6da1b2be1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2019
ms.locfileid: "54211008"
---
# <a name="lesson-4-2-create-a-corrupted-file"></a>第 4-2 课：创建损坏的文件

为阐释如何配置和处理转换错误，需要在处理时导致组件失败的示例平面文件。  
  
在本任务中，将创建现有示例平面文件的一个副本。 然后在记事本中打开该文件，并编辑“CurrencyID”列以包含错误的值，这会导致查找失败。 处理已损坏的文件时，查找失败将导致 Currency Key 查找转换失败，从而导致包的其余部分失败。 创建损坏的示例文件后，将运行包以查看包失败的情况。  
  
## <a name="create-a-corrupted-sample-flat-file"></a>创建损坏的示例平面文件  
  
1.  在记事本或任何其他文本编辑器中，打开“Currency_VEB.txt”文件。  
  
2.  使用文本编辑器的查找和替换功能，查找 **VEB** 的所有实例，并将其替换为 **BAD**。  
  
3.  在包含其他示例数据文件的同一文件夹中，将修改后的文件另存为 **Currency_BAD.txt**。  
  
    > [!NOTE]  
    > 确保将 Currency_BAD.txt 保存在与其他示例数据文件相同的文件夹中。  
  
4.  关闭文本编辑器。  
  
## <a name="verify-that-an-error-occurs-during-run-time"></a>验证运行时是否发生错误  
  
1.  在“调试”菜单中，选择“启动调试”。  
  
    在数据流第三次迭代中，Lookup Currency Key 转换尝试处理 Currency_BAD.txt 文件，并且转换失败。 转换失败导致整个包失败。  
  
2.  在“调试”菜单中，选择“停止调试”。  
  
3.  在设计图面上，选择“执行结果”选项卡。  
  
4.  浏览日志，确认是否发生了以下未处理的错误：  
  
    ```
    [Lookup Currency Key[27]] Error: Row yielded no match during lookup.
    ```
  
    > [!NOTE]  
    > 数字 27 为组件的 ID。 该值在生成数据流时进行分配，可能与包中的值不同。  
  
## <a name="go-to-next-task"></a>转到下一个任务  
[步骤 3：添加错误流重定向](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
  
  
