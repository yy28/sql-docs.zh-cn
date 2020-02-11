---
title: 过程调用中的参数标记 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bb24fb628e9e49fd94104af05217511a8f57c3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67912308"
---
# <a name="parameter-markers-in-procedure-calls"></a>过程调用中的参数标记
调用接受参数的过程时，可互操作的应用程序应使用参数标记，而不是文本参数值。 某些数据源不支持在过程调用中使用文字参数值。 有关参数的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。 有关调用过程的详细信息，请参阅本部分后面的[过程调用](../../../odbc/reference/develop-app/procedure-calls.md)。
