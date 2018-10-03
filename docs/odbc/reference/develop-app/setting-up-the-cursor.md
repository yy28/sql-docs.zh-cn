---
title: 设置游标 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59ade343f282933e05619996b119bc08e2dfb2ab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825515"
---
# <a name="setting-up-the-cursor"></a>设置游标
执行语句创建一个结果集之前，应用程序可以指定游标类型。 做到这一点与 SQL_ATTR_CURSOR_TYPE 语句属性。 如果应用程序未显式指定类型，将使用只进游标。 若要获取混合的游标，应用程序指定的由键集驱动游标，但不会早于结果集大小声明由键集大小。  
  
 对于由键集驱动和混合游标，该应用程序还可以指定由键集大小。 做到这一点与 SQL_ATTR_KEYSET_SIZE 语句属性。 如果由键集大小设置为 0，这是默认值，由键集大小设置为结果集大小，而使用由键集驱动的游标。 打开游标后，可以更改由键集大小。  
  
 应用程序还可以设置行集大小;有关详细信息，请参阅[使用块状游标](../../../odbc/reference/develop-app/using-block-cursors.md)前面在本部分中。
