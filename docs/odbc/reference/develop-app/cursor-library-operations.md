---
description: 游标库操作
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: efe3191e264fe45307ef90624f6b6e76d4ccaff6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429409"
---
# <a name="cursor-library-operations"></a>游标库操作
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 如果使用 ODBC 2.x 驱动程序的*应用程序对*odbc *1.x 游标库*进行调用，则该应用程序可能能够使用 odbc 2.x*驱动程序*不支持的 odbc *2.x 功能。* 不过，应用程序编写人员应小心地使用这些功能。 使用 ODBC *1.x 游标库*不会将 odbc 2.x 驱动程序设置*为 odbc 2.x* *驱动程序。*
