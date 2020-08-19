---
description: 记录集相关错误信息
title: 记录集相关的错误信息 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
author: rothja
ms.author: jroth
ms.openlocfilehash: 7806d446c200f4d90ec458ceea268435ad9994e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452949"
---
# <a name="recordset-related-error-information"></a>记录集相关错误信息
在批处理过程中， **recordset**对象的**Status**属性提供有关**记录集中**各个记录的信息。 在进行批更新之前，**记录集**的 "**状态**" 属性将反映与要添加、更改和删除的记录有关的信息。 调用 **UpdateBatch** 后， **状态** 属性指示操作是成功还是失败。 当您在记录 **集中**的记录之间移动时， **Status** 属性的值将更改以描述当前记录的状态。
