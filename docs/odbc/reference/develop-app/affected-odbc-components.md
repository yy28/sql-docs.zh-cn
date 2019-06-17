---
title: 受影响的 ODBC 组件 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72e004e6fd41ee74643fc05ec9020e6ac1933e09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186258"
---
# <a name="affected-odbc-components"></a>受影响的 ODBC 组件
向后兼容性介绍引入新版本的驱动程序管理器如何影响应用程序、 驱动程序管理器和驱动程序。 这会影响应用程序和驱动程序时或这两个文件保留在旧版本。 有，因此，三种类型的向后兼容性，还需要考虑以下表中所示。  
  
|类型|数据挖掘的版本|应用程序的版本|驱动程序版本|  
|----------|-------------------|----------------------------|-----------------------|  
|向后兼容的驱动程序管理器|3 *.x*|2.*x*|2.*x*|  
|向后兼容性驱动程序 [1]|3 *.x*|2.*x*|3.*x*|  
|应用程序的向后兼容性|3.*x*|3.*x*|2.*x*|  
  
 [在附录 g： 主要讨论驱动程序 1] 的向后兼容性为了向后兼容的驱动程序指南。  
  
> [!NOTE]
>  符合标准的应用程序-例如，已写入的 Open Group 或 ISO CLI 标准-根据应用程序保证适用于 ODBC 3 *.x*驱动程序通过 ODBC 3 *.x*驱动程序管理器。 假定应用程序使用的功能现已推出该驱动程序。 它还假定，符合标准的应用程序进行编译 ODBC 3 *.x*标头文件。
