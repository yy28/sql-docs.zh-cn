---
title: 受影响的 ODBC 组件 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d9155fa1c9df5846f069e93a3db1b969e9219ed
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306471"
---
# <a name="affected-odbc-components"></a>受影响的 ODBC 组件
向后兼容性描述应用程序、驱动程序管理器和驱动程序如何受到新版本驱动程序管理器的影响。 当应用程序和驱动程序都保留在旧版本中时，这会影响它们。 因此，需要考虑三种类型的向后兼容性，如下表所示。  
  
|类型|DM 版本|应用程序版本|驱动程序版本|  
|----------|-------------------|----------------------------|-----------------------|  
|驱动程序管理器的向后兼容性|*3.x*|*2.x*|*2.x*|  
|驱动程序的向后兼容性[1]|*3.x*|*2.x*|*3.x*|  
|应用程序向后兼容性|*3.x*|*3.x*|*2.x*|  
  
 [1] 驱动程序的向后兼容性主要在附录 G：向后兼容性驱动程序指南中讨论。  
  
> [!NOTE]
>  符合标准的应用程序（例如，已按照开放组或 ISO CLI 标准编写的应用程序）保证通过 ODBC *3.x*驱动程序管理器与 ODBC *3.x*驱动程序配合使用。 假定应用程序正在使用的功能在驱动程序中可用。 还假定符合标准的应用程序已使用 ODBC *3.x*标头文件进行编译。
