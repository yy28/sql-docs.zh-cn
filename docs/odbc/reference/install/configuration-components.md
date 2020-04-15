---
title: 配置组件 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], configuring
ms.assetid: 0b68ff48-12e4-41aa-b9e2-b39ed5023ea7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37c2518c3b18423c804631780ee4a18bff29d88b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289008"
---
# <a name="configuration-components"></a>配置组件
> [!NOTE]  
>  从 Windows XP 和 Windows 服务器 2003 开始，ODBC 包含在 Windows 操作系统中。 您只应在早期版本的 Windows 上显式安装 ODBC。  
  
 数据源由安装程序 DLL 配置，后者反过来调用驱动程序设置 DLL 和转换器根据需要设置 DLL。 安装程序 DLL 直接从控制面板调用，或者由另一个程序（称为*管理程序*）加载和调用。 下图显示了配置组件之间的关系。  
  
 ![配置组件之间的关系](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 有关这些组件的详细信息，请参阅本节末尾的以下主题。  
  
-   [安装程序](../../../odbc/reference/install/setup-program.md)  
  
-   [安装程序 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驱动程序安装程序 DLL](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>另请参阅  
 [安装组件](../../../odbc/reference/install/installation-components.md)
