---
title: 连接到 Microsoft Azure 存储 | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.windowsazurestorage.connect.f1
- SQL13.SWB.WINDOWSAZURESTORAGE.CONNECT.F1
ms.assetid: ''
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3e7f3a8d7168e9e1b9e321a83e7e1d7143b5bcf1
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265081"
---
# <a name="connect-to-microsoft-azure-storage"></a>连接到 Microsoft Azure 存储
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
可使用“Windows Azure 存储连接”  对话框指定存储帐户并验证与 Windows Azure 的连接。  
  
## <a name="options"></a>选项  
指定有关 Windows Azure 帐户的以下信息，然后单击“下一步”  继续。  
  
1.  **存储帐户** - 指定存储帐户名称。

   >[!NOTE]
   > 只能连接到[常规用途存储帐户](https://docs.microsoft.com/azure/storage/storage-introduction#azure-storage-services)。 连接到其他类型的存储帐户可能会导致如下错误：
   >
   >  其中一个 HTTP 标头的值格式不正确。 (Microsoft.SqlServer.StorageClient)。
   >
   >  远程服务器返回错误：(400) 错误的请求。 （系统）

2.  **帐户密钥** - 为指定的存储帐户指定帐户密钥。  
  
3.  **使用安全终结点 (HTTPS)** - 此选项利用网络 Web 服务器的加密通信和安全标识。  
  
4.  **保存帐户密钥** - 此选项可将密码保存在加密文件中。  
  
