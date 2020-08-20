---
description: 相关名称
title: 相关名称 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- correlation names [ODBC]
- SQL grammar [ODBC], correlation names
ms.assetid: 76c36c6f-f8e1-4ece-a77b-611dde3bdd8a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24de7ec65b069839541cfa5cd272a221ebc96ecd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471639"
---
# <a name="correlation-names"></a>相关名称
完全支持相关名称，包括在表列表中。 例如，在下面的字符串中，E1 是名为 Emp 的表的相关名称：  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```
