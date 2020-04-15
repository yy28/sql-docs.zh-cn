---
title: 附录 G：向后兼容性的驱动程序指南 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1055f94cb54bba9262f210e5df5f028029aebf5b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292397"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>附录 G：驱动程序后向兼容性准则
本附录为在 ODBC 3 上工作的驱动程序编写者提供信息。*x*需要支持 ODBC 2 的驱动程序。*x*应用程序。 有关向后兼容性的详细信息，请参阅[向后兼容性和标准合规性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 本部分包含以下主题。  
  
-   [块光标、可滚动光标和向后兼容性的 ODBC 3.x 驱动程序](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)- 新功能是 ODBC 3 中存在的功能。*x，* 而不是ODBC 2。*x*. . ODBC 3.*x*驱动程序通常不必担心与新功能的向后兼容性，因为 ODBC 2。*x*应用程序从不使用它们。 唯一的例外是与 SQLFetch、SQLFetchScroll、SQLSetPos**SQLSetPos**和 SQL**扩展获取**相关的功能。 **SQLFetch** **SQLFetchScroll**有关详细信息，请参阅 本附录后面的 。。  
  
-   [映射弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)- 重复功能是在 ODBC 3 中以不同的方式实现的功能。*x*和 ODBC 2。*x*. . ODBC 3.*x*驱动程序不必担心与重复的要素的向后兼容性，因为驱动程序管理器始终映射 ODBC 2。*x* ODBC 3 的功能。*x*调用 ODBC 3 时的功能。*x*驱动程序。 因此，ODBC 3。*x*驱动程序只能看到 ODBC 3。*x*功能。 有关这些映射的详细信息，请参阅 本附录后面的 。  
  
-   [行为更改和 ODBC 3.x 驱动程序](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md)- 行为更改是在 ODBC 3 中以不同的方式处理的功能。*x*和 ODBC 2。*x*. . ODBC 3.*x*驱动程序必须担心行为更改，并响应应用程序设置SQL_ATTR_ODBC_VERSION环境属性。
