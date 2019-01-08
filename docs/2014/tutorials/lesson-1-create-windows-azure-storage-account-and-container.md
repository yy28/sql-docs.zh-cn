---
title: 第 1 课：创建 Windows Azure 存储帐户和容器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: efdbd930-cde5-41b0-90ad-58a6cc68dddc
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: edeefac46805ba74b011d7c86202c7d5dbcdec14
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367149"
---
# <a name="lesson-1-create-windows-azure-storage-account-and-container"></a>第 1 课：创建 Windows Azure 存储帐户和容器
  必须先创建 Windows Azure 存储帐户和 blob 容器以及共享访问签名，然后才能将 SQL Server 数据文件存储在 Windows Azure 存储中。 第 1 课指导您完成登录到 Windows Azure 管理门户以及创建存储帐户、Blob 容器和共享访问签名的步骤。  
  
 默认情况下，只有存储帐户的所有者可访问该帐户内的 Blob、表和队列。 若要能够使用此项新的 SQL Server 增强在不共享存储帐户访问密钥的情况下访问这些资源，必须执行以下操作：  
  
-   将容器的权限设置为私有。  
  
-   创建共享访问签名。 通过它，可委派对容器、Blob、表或队列资源的受限访问权限，方法为指定间隔，期间这些资源可用，以及客户端将对这些资源拥有的权限。  
  
-   使用存储的访问策略管理容器或其 Blob 的共享访问签名。 存储的访问策略提供针对共享访问签名的另外一种控制措施，还提供一种撤消这些措施的简单方法。  
  
 有关详细信息，请参阅[管理对 Windows Azure 存储资源的访问](https://msdn.microsoft.com/library/windowsazure/ee393343.aspx)。  
  
## <a name="create-storage-account"></a>创建存储帐户  
 若要在 Windows Azure 管理门户上创建存储帐户，请执行以下步骤：  
  
1.  登录到[Windows Azure 管理门户](https://manage.windowsazure.com)使用你的帐户。 如果您没有 Windows Azure 帐户，请访问[Windows Azure 免费试用版](http://www.windowsazure.com/pricing/free-trial/)。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-1.gif "SQL 14 CTP2")  
  
2.  使用到的分步说明[创建存储帐户](http://azure.microsoft.com/documentation/articles/storage-create-storage-account/)。 注意，创建用于“Windows Azure 中的 SQL Server 数据文件”功能的存储帐户时，应取消选择或禁用地理复制。 这是因为对于参与地理复制的多个 Blob 无法保证写入顺序。 如果存储帐户经过地理复制，并且需要恢复，则发生损坏。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-2.gif "SQL 14 CTP2")  
  
## <a name="create-a-blob-container"></a>创建 Blob 容器  
 在 Windows Azure 中，容器用于集中一组 Blob。 所有 Blob 必须都在一个容器中。 一个存储帐户可含有无限数量的容器，但必须至少有一个容器。 一个容器可以存储无限数量的 Blob。 存储大小限制的最新信息，请参阅[如何在.NET 中使用 Windows Azure Blob 存储服务](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)。  
  
 若要在 Windows Azure 中创建容器，请执行以下步骤：  
  
1.  登录到[Windows Azure 管理门户](https://manage.windowsazure.com)。  
  
2.  选择存储帐户中，单击**容器**选项卡，单击**添加容器**在屏幕的底部，这会打开新建对话框。  
  
3.  输入容器的名称。  
  
4.  选择**私有**有关**访问类型**。 将访问权限设置为专用后，只有 Windows Azure 帐户所有者可读取容器和 Blob 数据。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-4.gif "SQL 14 CTP2")  
  
> [!NOTE]  
>  若要以编程方式创建容器，还可使用 REST API。 有关详细信息，请参阅[创建容器](https://msdn.microsoft.com/library/windowsazure/dd179468.aspx)以及[Windows Azure 存储服务 REST API 参考](https://msdn.microsoft.com/library/windowsazure/dd179355.aspx)。  
  
 **下一课：**  
  
 [第 2 课.在容器上创建策略并生成共享访问签名&#40;SAS&#41;键](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)  
  
  
