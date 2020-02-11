---
title: 更改类型 |Microsoft Docs
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
ms.openlocfilehash: 5f43dbf75754a16b3163bbb8e268400f34d372b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087808"
---
# <a name="types-of-changes"></a>更改的类型
在 ODBC 2.x 中进行三种类型的更改（和任何版本*的 odbc）* 。 其中每个都会对向后兼容性产生不同的影响并以不同的方式进行处理。 下表描述了这些更改。  
  
|更改类型|说明|  
|--------------------|-----------------|  
|新增功能|这些*是 ODBC 3.x*的新手功能，如行外绑定或描述符。 仅当应用程序和驱动程序以及驱动程序管理器*的版本为*1.x 时才实现这些设置，因此，不会尝试使它们向后兼容。|  
|重复的功能|这些*是 odbc* 2.X 和 odbc 2.x 中存在的*功能，但*它们的实现方式不同。 函数**SQLAllocHandle**和**SQLAllocStmt**是一个示例。 这些功能和其他复制功能的向后兼容性问题大多由驱动程序管理器中的映射来处理。|  
|行为变更|这些功能在 ODBC *2.x 和 odbc* 2.x 中的处理方式*不同。* Datetime **#define**是一个示例。 这些功能*由 ODBC 1.x*驱动程序根据环境属性设置进行处理。 （有关详细信息，请参阅[行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)。）|
