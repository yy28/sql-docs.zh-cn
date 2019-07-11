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
ms.openlocfilehash: ca1b0fc2f7a1a74e1b9ab9a85baba945e4edf491
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792952"
---
# <a name="types-of-changes"></a>更改的类型
ODBC 中所做的更改的三种类型*3.x* （和 ODBC 的任何版本）。 其中每项功能以不同的方式会影响后向兼容性，并且以不同方式处理。 这些更改以下表所述。  
  
|更改类型|描述|  
|--------------------|-----------------|  
|新增功能|这些是功能的新 ODBC *3.x*，例如的外部绑定或描述符。 这些功能实现仅当应用程序和驱动程序，以及驱动程序管理器中，为版本*3.x*，因此不会尝试进行这些向后兼容。|  
|重复的功能|这些是在 ODBC 中存在的功能*2.x*和 ODBC *3.x* ，但在每个不同的方式实现。 函数**SQLAllocHandle**并**SQLAllocStmt**就是一个示例。 向后兼容性问题的这些和其他重复的功能主要是由驱动程序管理器中的映射。|  
|行为更改|这些是以不同的方式在 ODBC 中处理的功能*2.x*和 ODBC *3.x*。 日期时间 **#define**是一个示例。 这些功能将由 ODBC *3.x*驱动程序基于环境属性设置。 (请参阅[行为的更改](../../../odbc/reference/develop-app/behavioral-changes.md)有关详细信息。)|
