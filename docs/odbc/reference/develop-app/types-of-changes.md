---
title: 类型的更改 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac4d791bd848369ddeb87209676c65d639506af6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="types-of-changes"></a>类型的更改
三种类型的更改都在 ODBC 3。*x* （和 ODBC 的任何版本）。 其中每个以不同的方式会影响向后兼容性，并且以不同的方式处理。 这些更改以下表所述。  
  
|更改类型|Description|  
|--------------------|-----------------|  
|新增功能|这些是对 ODBC 3 不熟悉的功能。*x*，如超行绑定或描述符。 这些功能实现仅当应用程序和驱动程序，以及驱动程序管理器中，均为版本 3 时，才 *.x*，因此没有尝试进行这些向后兼容。|  
|重复的功能|这些是 ODBC 2 中存在的功能 *.x*和 ODBC 3。*x*但在每个不同的方式实现。 函数**SQLAllocHandle**和**SQLAllocStmt**是一个示例。 向后兼容性问题对于这些和其他重复的功能主要由映射驱动程序管理器中。|  
|行为更改|这些是在 ODBC 2 中处理方式则不同的功能 *.x*和 ODBC 3。*x*。 Datetime **#define**是一个示例。 这些功能由 ODBC 3 处理。*x*驱动程序以环境属性设置。 (请参阅[行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)有关详细信息。)|
