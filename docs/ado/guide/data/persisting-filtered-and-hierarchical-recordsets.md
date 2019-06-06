---
title: 保存的筛选和分层记录集 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cbd237580dc8c56284552e6fe2fb00e469832c5b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702044"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>保留筛选记录集和分层记录集
如果[筛选器](../../../ado/reference/ado-api/filter-property.md)属性实际上是有关**记录集**，保存筛选器下可访问的行。 如果**记录集**是分层的当前子**记录集**和及其子级都得到保存，包括父**记录集**。 如果**保存**方法的子**记录集**是调用，保存子及其所有子级，但不是父级。 有关层次结构的详细信息**记录集**，请参阅[数据整理](../../../ado/guide/data/data-shaping.md)。  
  
> [!NOTE]
>  保存层次结构时，将应用一些限制**记录集**（数据形状） 以 XML 格式。 有关详细信息，请参阅[以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)。
