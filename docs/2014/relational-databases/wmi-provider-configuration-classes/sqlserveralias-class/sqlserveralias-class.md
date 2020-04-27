---
title: SqlServerAlias 类 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- SqlServerAlias Class
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SqlServerAlias class
ms.assetid: 475662b9-6985-45bf-b1e9-b0f26ef50443
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0ffbf733db8cbd672f171773e7b44560686e7d1a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63223550"
---
# <a name="sqlserveralias-class"></a>SqlServerAlias 类
  [SqlServerAlias 类](sqlserveralias-class.md)表示服务器连接别名。  
  
 出现以下两种情况时需要服务器连接别名：  
  
-   客户端[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]通过网络传输连接到不是默认网络传输的实例。  
  
-   客户端连接到的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例侦听备用命名管道。  
  
 **注意：**[SqlServerAlias 类](sqlserveralias-class.md)从 Provider 类`Put`继承方法。 但是，与 `Provider::Put` 方法不同，它不会返回任何结果。 有关详细信息，请参阅 WMI 文档。  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
