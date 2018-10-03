---
title: 游标库操作 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32e3fcaf9c83c2613a1dc2df499f11c7df2570ad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692395"
---
# <a name="cursor-library-operations"></a>游标库操作
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 如果应用程序使用 ODBC 2 *.x*驱动程序，可以对 ODBC 3 的调用。*x*游标库，应用程序可能无法使用 ODBC 3。*x*不支持 ODBC 2 的功能 *.x*驱动程序。 这些功能的使用方式，但是一定要小心应用程序编写器。 使用 ODBC 3。*x*游标库不会使 ODBC 2 *.x* ODBC 3 到驱动程序。*x*驱动程序。
