---
description: UPDATE 语句限制
title: UPDATE 语句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b7c1ea2e5e9d887005084cdb5454dcf9b5e8fa24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471396"
---
# <a name="update-statement-limitations"></a>UPDATE 语句限制
为了使 Paradox 驱动程序更新表，表必须具有唯一索引 (Paradox 主键) 。 使用 Paradox 驱动程序时，如果不实现 Borland 数据库引擎，将无法更新 Paradox 表。  
  
 不受文本驱动程序支持。  
  
 当使用 Microsoft Excel 驱动程序时，可能会更新值，但无法基于 Microsoft Excel 电子表格从表中删除行。 因此，Microsoft Excel 驱动程序不会将 UPDATE 语句视为正式支持。 仅将 INSERT 语句视为受支持。
