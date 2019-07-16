---
title: 编辑现有记录 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ce8679c0c7b20dfaa641918f0447a2f77bfd474a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925441"
---
# <a name="editing-existing-records"></a>编辑现有记录
若要编辑现有记录，将移动到想要编辑或更改的行**值**你想要更改的字段的属性。 有关详细信息**字段**对象的**值**属性，请参阅[检查数据](../../../ado/guide/data/examining-data.md)。 具体取决于游标类型，将使用**更新**或**UpdateBatch**若要将更改发送回数据源。 有关详细信息，请参阅[更新和保存数据](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
 它是用于存储的过程的一个命令对象执行更新，以及方式来执行其他操作，因为存储的过程不需要创建游标通常更高效。 有关游标的详细信息，请参阅[了解游标和锁定](../../../ado/guide/data/understanding-cursors-and-locks.md)。
