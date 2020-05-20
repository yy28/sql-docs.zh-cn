---
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
ms.openlocfilehash: 5fa3fdd55fb78f16629907c174b08aab64ceb86e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763108"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>保留筛选记录集和分层记录集
如果[筛选器](../../../ado/reference/ado-api/filter-property.md)属性对**记录集**有效，则仅保存在筛选器下可访问的行。 如果**记录集**是分层的，则保存当前子**记录集**及其子记录集（包括父**记录集**）。 如果调用子记录集的**Save**方法，则会保存子记录集及其所有子级，但不会保存父**记录集**。 有关分层**记录集**的详细信息，请参阅[数据定形](../../../ado/guide/data/data-shaping.md)。  
  
> [!NOTE]
>  在以 XML 格式保存分层**记录集**（数据形状）时，有一些限制。 有关详细信息，请参阅[以 XML 格式保存记录](../../../ado/guide/data/persisting-records-in-xml-format.md)。
