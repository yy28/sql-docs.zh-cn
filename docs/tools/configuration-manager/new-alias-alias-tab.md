---
title: "新别名 （别名选项卡） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 785eb6fb-f67e-449d-b1c8-c38dfbb95ef6
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 988ee74394f53d5275a8b8e1cc3772702792a4f3
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="new-alias-alias-tab"></a>新建别名（“别名”选项卡）
  别名是可用于进行连接的备用名称。 别名封装了连接字符串所必需的元素，并使用用户所选择的名称显示这些元素。 使用“别名 - 新建”对话框中的“别名”页可以指定别名连接字符串的元素。 若要更改现有别名的连接字符串，请参阅 [<别名> 属性（别名选项卡）](../../tools/configuration-manager/alias-properties-alias-tab.md)。  
  
 无需在 **“属性”** 的所有网格中都填写值。 有效组合因所选协议的不同而有所变化。 请参阅下面列出的有关有效组合示例的主题。  
  
 **别名**  
 用于引用此连接的名称（别名）。  
  
 **管道名称** / **端口号**  
 连接字符串的其他元素。 此框的名称随所选协议的不同而变化。  
  
 **协议**  
 连接所用的协议。  
  
 **Server**  
 所连接的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。  
  
## <a name="when-to-use-an-alias"></a>何时使用别名  
 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] “共享内存” **协议连接到** 的本地实例，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] “TCP/IP” **或** “命名管道” **连接到其他计算机上的**实例。 请在以下情况下创建别名：使用 TCP/IP 或命名管道，并且希望提供自定义连接字符串时；希望使用服务器名称之外的其他名称进行连接时。  
  
### <a name="examples"></a>示例  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会侦听默认 TCP/IP 端口 1433，因此您希望提供一个包含另一端口号的连接字符串。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会侦听默认命名管道，因此您希望提供一个包含不同管道名称的连接字符串。  
  
-   希望将应用程序连接到名为 `ACCT`的服务器上的数据库，但该数据库已合并为名为 `ACCT` 的服务器上的 `CENTRAL`实例。 该应用程序不能轻易更改。 创建一个别名 `ACCT`，其中包含指向 `CENTRAL\ACCT`的连接字符串。  
  
## <a name="creating-a-valid-connection-string"></a>创建有效连接字符串  
 有关别名属性的有效组合的说明和示例，请参阅下列主题：  
  
-   [创建有效的连接字符串使用 Shared 的 Memory 协议](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
-   [创建使用 TCP IP 有效的连接字符串](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)  
  
-   [创建有效的连接字符串使用命名的管道](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)  
  
  
