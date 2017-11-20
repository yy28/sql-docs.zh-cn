---
title: "附录 g： 为了向后兼容驱动程序准则 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e326abbc0a10899028bf93d27f219fadd8d7dd29
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>为了向后兼容的附录 g： 驱动程序准则
本附录提供驱动程序编写器处理 ODBC 3 的信息。*x*驱动程序需要支持 ODBC 2。*x*应用程序。 有关向后兼容性的详细信息，请参阅[向后兼容性和标准合规性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 本部分包含以下主题。  
  
-   [块状游标可滚动游标，ODBC 3.x 驱动程序的向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)-新功能是 ODBC 3 中存在的功能。*x* ，不能在 ODBC 2。*x*。 ODBC 3。*x*驱动程序通常不必担心与新功能的向后兼容性，因为 ODBC 2。*x*应用程序永远不会使用它们。 唯一的例外是与相关的功能**SQLFetch**， **SQLFetchScroll**， **SQLSetPos**，和**SQLExtendedFetch**; 有关详细信息信息，请参阅，此附录中更高版本。  
  
-   [映射弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)-重复功能是在 ODBC 3 中以不同方式实现的功能。*x*和 ODBC 2。*x*。 ODBC 3。*x*驱动程序无需担心具有重复功能的向后兼容性，因为驱动程序管理器始终映射 ODBC 2。*x* ODBC 3 的功能。*x*功能时调用 ODBC 3。*x*驱动程序。 因此，一个 ODBC 3。*x*驱动程序会看到仅 ODBC 3。*x*功能。 有关详细信息这些映射，此附录中更高版本，请参阅。  
  
-   [行为更改和 ODBC 3.x 驱动程序](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md)-行为更改是在 ODBC 3 中处理方式则不同的功能。*x*和 ODBC 2。*x*。 ODBC 3。*x*驱动程序需要担心行为更改，并以响应由应用程序设置的 SQL_ATTR_ODBC_VERSION 环境属性执行操作。

