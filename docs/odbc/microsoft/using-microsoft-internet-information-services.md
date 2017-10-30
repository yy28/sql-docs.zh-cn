---
title: "使用 Microsoft Internet 信息服务 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 75659769b4d0318fa21494a3f2ca3262836c69eb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-microsoft-internet-information-services"></a>使用 Microsoft Internet 信息服务
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 如果您不了解从 IIS 脚本 （尤其是当你收到 ORA 12641 出错） 中的连接，请将以下行添加到 Sqlnet.ora 文件：  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 这将禁用安全网络服务，因此你可以使用匿名身份验证进行连接。

