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
ms.openlocfilehash: 08997f610b00f22d436a5c91d34beb2a8fc2cc1d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67944856"
---
# <a name="affected-odbc-components"></a>受影响的 ODBC 组件
向后兼容性介绍了驱动程序管理器的新版本引入了应用程序、驱动程序管理器和驱动程序的影响。 当应用程序和驱动程序在旧版本中保留时，这会影响应用程序和驱动程序。 因此，需要考虑三种类型的向后兼容性，如下表所示。  
  
|类型|DM 版本|应用程序的版本|驱动程序版本|  
|----------|-------------------|----------------------------|-----------------------|  
|驱动程序管理器的向后兼容性|*3.x*|*2.x*|*2.x*|  
|驱动程序的向后兼容性 [1]|*3.x*|*2.x*|*3.x*|  
|应用程序的向后兼容性|*3.x*|*3.x*|*2.x*|  
  
 [1] 驱动程序的向后兼容性主要在附录 G：驱动程序准则中讨论，以便向后兼容。  
  
> [!NOTE]
>  符合标准的应用程序（例如，根据开放组或 ISO CLI 标准编写的应用程序）保证通过 ODBC 2.x 驱动程序管理器*与 odbc 1.x* *驱动程序*一起工作。 假定应用程序正在使用的功能在驱动程序中可用。 它还假定符合标准的应用程序已编译*为 ODBC 3.x*标头文件。
