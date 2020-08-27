---
description: 编辑现有记录
title: 编辑现有记录 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
author: rothja
ms.author: jroth
ms.openlocfilehash: 35c2376031e96a19c4a761a9826e47be2306518e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991328"
---
# <a name="editing-existing-records"></a>编辑现有记录
若要编辑现有记录，请转到要编辑的行，然后更改要更改的字段的 **值** 属性。 有关 **字段** 对象的 **Value** 属性的详细信息，请参阅 [检查数据](./examining-data.md)。 根据游标类型，您将使用 **Update** 或 **UpdateBatch** 将更改发送回数据源。 有关详细信息，请参阅 [更新和保留数据](./updating-and-persisting-data.md)。  
  
 通常，将存储过程与命令对象结合使用来执行更新，以及执行其他操作，这种方法通常更高效，因为存储过程不需要创建游标。 有关游标的详细信息，请参阅 [了解游标和锁定](./understanding-cursors-and-locks.md)。