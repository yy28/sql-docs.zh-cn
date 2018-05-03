---
title: 错误 (ADO) |Microsoft 文档
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
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 8ae6611b-3069-4155-b014-c0c9da37be39
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d23582c5700f5d528f0b16f45e43aba01ec7f405
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="errors-ado"></a>错误 (ADO)
涉及 ADO 对象的任何操作可以生成一个或多个提供程序错误。 每个错误发生时，一个或多个**错误**对象都将置于**错误**集合**连接**对象。 有关处理警告和 ADO 应用程序中的错误的详细信息，请参阅[错误处理](../../../ado/guide/data/error-handling.md)。  
  
 可以通过单独的机制会引发应用程序错误。 例如，在 Visual Basic 中， **Err**对象将包含应用程序级错误。
