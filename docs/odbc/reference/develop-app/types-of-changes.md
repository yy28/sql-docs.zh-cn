---
title: 更改类型 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f44adb59aa9b0f25475a76a97fe3670de0228c08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301602"
---
# <a name="types-of-changes"></a>更改的类型
在 ODBC *3.x（* 以及任何版本的 ODBC）中进行了三种类型的更改。 其中每种方法对向后兼容性的影响都不同，并且以不同的方式处理。 下表描述了这些更改。  
  
|更改类型|描述|  
|--------------------|-----------------|  
|新增功能|这些是 ODBC *3.x*的新功能，例如行外绑定或描述符。 仅当应用程序和驱动程序以及驱动程序管理器版本*3.x*时，才会实现这些版本，因此不会尝试使这些向后兼容。|  
|重复的功能|这些功能存在于 ODBC *2.x*和 ODBC *3.x*中，但在每个功能中以不同的方式实现。 **SQLAllocHandle**和**SQLAllocStmt**的函数就是一个例子。 这些和其他重复功能的向后兼容性问题主要由驱动程序管理器中的映射处理。|  
|行为变更|这些功能在 ODBC *2.x*和 ODBC *3.x*中处理方式不同。 日期时间 **#define**就是一个例子。 这些功能由 ODBC *3.x*驱动程序根据环境属性设置处理。 （有关详细信息，请参阅[行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)。|
