---
title: 设置光标 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 805d8076c853513d86f9a3a92d9342d1224226c9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299797"
---
# <a name="setting-up-the-cursor"></a>设置游标
应用程序可以在执行创建结果集的语句之前指定游标类型。 它使用SQL_ATTR_CURSOR_TYPE语句属性进行此用。 如果应用程序未显式指定类型，将使用仅转发游标。 要获取混合游标，应用程序指定键集驱动的游标，但声明键集大小小于结果集大小。  
  
 对于键集驱动和混合游标，应用程序还可以指定键集大小。 它使用SQL_ATTR_KEYSET_SIZE语句属性进行此用。 如果键集大小设置为 0（默认值），则键集大小设置为结果集大小，并使用键集驱动的游标。 打开游标后，可以更改键集大小。  
  
 应用程序还可以设置行集大小;因此，应用程序还可以设置行集大小。有关详细信息，请参阅本节前面部分使用[块光标](../../../odbc/reference/develop-app/using-block-cursors.md)。
