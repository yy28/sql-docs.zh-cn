---
title: 记录集相关的错误信息 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 142177831126100343a293bb1467726dcd0e29e0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="recordset-related-error-information"></a>记录集相关的错误信息
在批处理、 过程**状态**属性**记录集**对象提供有关中的单个记录的信息**记录集**。 批处理更新发生之前**状态**属性**记录集**反映有关要添加、 更改和删除记录的信息。 后**UpdateBatch**已调用**状态**属性指示该操作成功与否。 移动在记录间**记录集**的值**状态**属性更改，以描述当前记录的状态。
