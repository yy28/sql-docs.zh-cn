---
title: 预测错误 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5978768e515f4fc6cf6986dc23e7cec1379c69c7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="anticipating-errors"></a>预测错误
错误防护是至少与错误处理一样重要。 此最后一节包含一个你的应用程序可以帮助进行不太可能发生的错误的预防措施的简短列表。  
  
 通过签入的值来检查对象的状态**状态**然后再尝试使用这些对象执行操作的属性。 例如，如果你的应用程序使用全局**连接**，检查其**状态**属性以查看它是否已打开之前调用**打开**方法。  
  
-   接受来自用户的数据的任何程序必须包含代码，从而将其发送到数据存储区之前验证该数据。 你不能依赖于数据存储、 提供程序、 ADO 或甚至是您的编程语言，若要向你通知问题。 必须检查输入你的用户，并确保数据是其字段的正确类型和必填的字段都不为空的每个字节。  
  
 尝试将任何数据写入到数据存储区之前，请检查数据。 若要这样做的最简单方法是处理**WillMove**事件或**WillUpdateRecordset**事件。 有关处理 ADO 事件的更完整讨论，请参阅[处理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)。  
  
 请确保**记录集**对象是否不超出边界**记录集**之前尝试移动记录指针。 如果您尝试对**MoveNext**时**EOF**为 True 或**MovePrev**时**BOF**为 True 时，将会出错。 如果你执行任何**移动**方法时同时**EOF**和**BOF**都为 True，将生成错误。  
  
 此外将发生错误如果你尝试执行操作，如**Seek**和**查找**上一个空**记录集**。
