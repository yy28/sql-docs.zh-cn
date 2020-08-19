---
description: 保留筛选记录集和分层记录集
title: 保持筛选和分层记录集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
author: rothja
ms.author: jroth
ms.openlocfilehash: a69b491f4bb5834331b9cfa582b6f72d248ba317
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453059"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>保留筛选记录集和分层记录集
如果 [筛选器](../../../ado/reference/ado-api/filter-property.md) 属性对 **记录集**有效，则仅保存在筛选器下可访问的行。 如果 **记录集** 是分层的，则保存当前子 **记录集** 及其子记录集（包括父 **记录集**）。 如果调用子记录集的 **Save** 方法，则会保存子记录集及其所有子级，但不会保存父 **记录集** 。 有关分层 **记录集**的详细信息，请参阅 [数据定形](../../../ado/guide/data/data-shaping.md)。  
  
> [!NOTE]
>  在将分层 **记录集** 保存 () XML 格式的数据形状时，有一些限制。 有关详细信息，请参阅 [以 XML 格式保存记录](../../../ado/guide/data/persisting-records-in-xml-format.md)。
