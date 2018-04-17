---
title: SqlServerAlias 类 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SqlServerAlias Class
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServerAlias class
ms.assetid: 475662b9-6985-45bf-b1e9-b0f26ef50443
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6ec80097c8e6af6d3cdf7af7adea2355347e99df
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserveralias-class"></a>SqlServerAlias 类
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [SqlServerAlias 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)类表示的服务器连接别名。  
  
 出现以下两种情况时需要服务器连接别名：  
  
-   客户端连接到的实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]通过网络传输不是默认网络传输。  
  
-   客户端连接到的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例侦听备用命名管道。  
  
 **注意：** [SqlServerAlias 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)继承**放**从提供程序类的方法。 但是，它不返回任何结果由**Provider::Put**方法。 有关详细信息，请参阅 WMI 文档。  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
