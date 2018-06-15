---
title: 相关名称 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- correlation names [ODBC]
- SQL grammar [ODBC], correlation names
ms.assetid: 76c36c6f-f8e1-4ece-a77b-611dde3bdd8a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d41b44ddd685cf911fa84f240f193cc39ddbcd1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32897672"
---
# <a name="correlation-names"></a>相关名称
完全支持相关名称，包括表列表中。 例如，以下字符串中 E1 是名为 Emp 的表的相关名：  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```
