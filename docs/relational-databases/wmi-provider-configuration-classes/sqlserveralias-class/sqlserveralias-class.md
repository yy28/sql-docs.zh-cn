---
description: SqlServerAlias 类
title: SqlServerAlias 类
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- SqlServerAlias Class
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServerAlias class
ms.assetid: 475662b9-6985-45bf-b1e9-b0f26ef50443
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 48ecf56931682da1ba0cc7ee1e379ad5146479db
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891627"
---
# <a name="sqlserveralias-class"></a>SqlServerAlias 类
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [SqlServerAlias 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)表示服务器连接别名。  
  
 出现以下两种情况时需要服务器连接别名：  
  
-   客户端 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通过网络传输连接到不是默认网络传输的实例。  
  
-   客户端连接到的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例侦听备用命名管道。  
  
 **注意：**[SqlServerAlias 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)从 Provider 类继承**Put**方法。 但是，它不会返回提供程序所指示的任何结果 **：:P** 工作身份方法。 有关详细信息，请参阅 WMI 文档。  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
