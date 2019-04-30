---
title: 类型的更改 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac92c6d40ea9ead6b8875e3338bb740b4bdf8523
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473174"
---
# <a name="types-of-changes"></a>更改的类型
在 ODBC 3 进行三种类型的更改。*x* （和 ODBC 的任何版本）。 其中每项功能以不同的方式会影响后向兼容性，并且以不同方式处理。 这些更改以下表所述。  
  
|更改类型|Description|  
|--------------------|-----------------|  
|新增功能|这些是为 ODBC 3 新增的功能。*x*，例如的外部绑定或描述符。 这些功能实现仅当应用程序和驱动程序，以及驱动程序管理器中，为版本 3 *.x*，因此不会尝试进行这些向后兼容。|  
|重复的功能|这些是存在于 ODBC 2 中的功能 *.x* ODBC 3。*x* ，但在每个不同的方式实现。 函数**SQLAllocHandle**并**SQLAllocStmt**就是一个示例。 向后兼容性问题的这些和其他重复的功能主要是由驱动程序管理器中的映射。|  
|行为更改|这些是 ODBC 2 中以不同方式处理的功能 *.x* ODBC 3。*x*。 日期时间 **#define**是一个示例。 这些功能由 ODBC 3 处理。*x*驱动程序基于环境属性设置。 (请参阅[行为的更改](../../../odbc/reference/develop-app/behavioral-changes.md)有关详细信息。)|
