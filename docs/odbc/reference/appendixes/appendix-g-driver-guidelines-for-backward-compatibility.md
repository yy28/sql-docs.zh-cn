---
title: 附录 G：为了向后兼容的驱动程序指南 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d78de7b3bd1d91351a4159847d6605e30cc1353d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026627"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>附录 G：驱动程序后向兼容性准则
本附录提供了驱动程序编写人员致力于 ODBC 3 的信息。*x*需要支持 ODBC 2 的驱动程序。*x*应用程序。 有关向后兼容性的详细信息，请参阅[向后兼容性和标准符合性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 本部分包含以下主题。  
  
-   [块游标、 可滚动游标和 ODBC 3.x 驱动程序的向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)的新功能是在 ODBC 3 中存在的功能。*x*而不是在 ODBC 2。*x*。 ODBC 3。*x*驱动程序通常不需要担心向后兼容的新功能，因为 ODBC 2。*x*应用程序永远不会使用它们。 唯一的例外是与相关的功能**SQLFetch**， **SQLFetchScroll**， **SQLSetPos**，以及**SQLExtendedFetch**; 有关详细信息信息，请参阅本附录中更高版本。  
  
-   [不推荐使用的函数映射](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)-重复的功能是在 ODBC 3 中以不同方式实现的功能。*x*以及 ODBC 2。*x*。 ODBC 3。*x*驱动程序不需要担心向后兼容的重复的功能，因为驱动程序管理器总是映射 ODBC 2。*x* ODBC 3 的功能。*x*功能时调用 ODBC 3。*x*驱动程序。 因此，ODBC 3。*x*驱动程序会看到仅 ODBC 3。*x*功能。 详细了解这些映射，请参阅本附录中更高版本。  
  
-   [行为更改和 ODBC 3.x 驱动程序](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md)的行为更改是在 ODBC 3 中以不同方式处理的功能。*x*以及 ODBC 2。*x*。 ODBC 3。*x*驱动程序需要担心的行为更改，并响应应用程序设置的 SQL_ATTR_ODBC_VERSION 环境属性。
