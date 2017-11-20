---
title: "获取描述符处理 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb3d75a78a5eaa516921e561cb2d34786804d182
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="obtaining-descriptor-handles"></a>获取描述符处理
应用程序作为输出参数的调用中获取的任何显式分配的描述符句柄**SQLAllocHandle**。 通过调用获得的隐式分配的描述符句柄**SQLGetStmtAttr**。

