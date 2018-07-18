---
title: 在过程调用中的参数标记 |Microsoft 文档
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
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d21de0ce752296e1534b01c197f18934862eec85
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910502"
---
# <a name="parameter-markers-in-procedure-calls"></a>在过程调用中的参数标记
当调用接受参数的过程，可互操作的应用程序应使用参数标记，而不是文本的参数值。 某些数据源不支持在过程调用中使用的文字参数值。 有关参数的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。 有关调用过程的详细信息，请参阅[过程调用](../../../odbc/reference/develop-app/procedure-calls.md)，本部分中更高版本。
