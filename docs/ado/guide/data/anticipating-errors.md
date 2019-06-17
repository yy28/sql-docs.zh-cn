---
title: 预测错误 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6e555f00964ae6bdc7eb91a8701f2447d91b37d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702411"
---
# <a name="anticipating-errors"></a>预测错误
错误防护是至少与错误处理一样重要。 此最后一节包含一个应用程序以使不太可能发生的错误而可以采取预防措施的简短列表。  
  
 通过检查的值检查对象的状态**状态**然后再尝试使用这些对象执行操作的属性。 例如，如果你的应用程序使用全局**连接**，检查其**状态**属性以查看它是否已打开之前调用**打开**方法。  
  
-   接受来自用户的数据的任何程序必须包含代码以将其发送到数据存储区之前验证该数据。 不能依赖于数据存储区、 提供程序、 ADO 中或甚至您的编程语言，以向你通知问题。 您必须检查输入的用户，并确保数据是正确的类型为其字段和必填的字段不为空的每个字节。  
  
 在尝试将任何数据写入到数据存储区之前，请检查的数据。 若要执行此操作的最简单方法是处理**WillMove**事件或**WillUpdateRecordset**事件。 处理 ADO 事件的更完整介绍，请参阅[处理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)。  
  
 请确保**记录集**对象是否不到的边界之外**记录集**然后再尝试将记录指针移动。 如果您尝试对**MoveNext**时**EOF**为 True 或**MovePrev**时**BOF**为 True 时，将会出错。 如果执行的任何**移动**方法时同时**EOF**并**BOF**均为 True，将生成错误。  
  
 也将会发生错误如果你尝试执行以下操作**Seek**并**查找**对空**记录集**。
