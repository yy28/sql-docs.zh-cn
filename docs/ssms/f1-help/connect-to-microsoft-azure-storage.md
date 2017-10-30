---
title: "连接到 Microsoft Azure 存储 | Microsoft Docs"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.windowsazurestorage.connect.f1
- SQL13.SWB.WINDOWSAZURESTORAGE.CONNECT.F1
ms.assetid: 
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: ea0fbb6f0297dfdbe94974de472c7a48ce8ce831
ms.openlocfilehash: b673559a735d3b28d6055a1440183861b3db692a
ms.contentlocale: zh-cn
ms.lasthandoff: 07/31/2017

---
# <a name="connect-to-microsoft-azure-storage"></a>连接到 Microsoft Azure 存储
可使用“Windows Azure 存储连接”对话框指定存储帐户并验证与 Windows Azure 的连接。  
  
## <a name="options"></a>选项  
指定有关 Windows Azure 帐户的以下信息，然后单击“下一步”继续。  
  
1.  **存储帐户** - 指定存储帐户名称。

   >[!NOTE]
   > 只能连接到[常规用途存储帐户](https://docs.microsoft.com/en-us/azure/storage/storage-introduction#introducing-the-azure-storage-services)。 连接到其他类型的存储帐户可能会导致如下错误：
   >
   >  其中一个 HTTP 标头的值格式不正确。 (Microsoft.SqlServer.StorageClient)。
   >
   >  远程服务器返回错误：(400)错误的请求。 （系统）

2.  **帐户密钥** - 为指定的存储帐户指定帐户密钥。  
  
3.  **使用安全端点 (HTTPS)** - 此选项利用网络 Web 服务器的加密通信和安全标识。  
  
4.  **保存帐户密钥** - 此选项可将密码保存在加密文件中。  
  

