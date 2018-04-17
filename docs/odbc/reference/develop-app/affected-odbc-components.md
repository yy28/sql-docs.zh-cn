---
title: 受影响的 ODBC 组件 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb58971a193a210f927d1b0a38f2be671b749468
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="affected-odbc-components"></a>受影响的 ODBC 组件
向后兼容性介绍的新版本的驱动程序管理器简介如何影响应用程序、 驱动程序管理器和驱动程序。 这会影响应用程序和驱动程序时这两个或其中任何一个保留在旧版本。 有，因此，三种类型的向后兼容性，还需要考虑下表中所示。  
  
|类型|版本的数据挖掘|应用程序版本|驱动程序的版本|  
|----------|-------------------|----------------------------|-----------------------|  
|向后兼容的驱动程序管理器|3*.x*|2。*x*|2。*x*|  
|后向兼容性驱动程序 [1]|3*.x*|2。*x*|3。*x*|  
|后向兼容性应用程序|3。*x*|3。*x*|2。*x*|  
  
 [1] 的向后兼容性驱动程序是主要讨论附录 g： 驱动程序准则中向后兼容性。  
  
> [!NOTE]  
>  符合标准的应用程序 — 例如，应用程序已根据 Open Group 或 ISO CLI 标准写入-保证适用于 ODBC 3*.x*驱动程序通过 ODBC 3*.x*驱动程序管理器。 假定应用程序使用的功能是驱动程序中可用。 另外，还假设，符合标准的应用程序具有带 ODBC 3 中编译*.x*标头文件。
