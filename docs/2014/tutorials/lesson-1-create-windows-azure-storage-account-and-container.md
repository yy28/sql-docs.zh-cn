---
title: 第 1 课：创建 Azure 存储帐户和容器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: efdbd930-cde5-41b0-90ad-58a6cc68dddc
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 69d09b5b058af3404226905bdbe0ef83f33982cf
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176175"
---
# <a name="lesson-1-create-azure-storage-account-and-container"></a>第 1 课：创建 Azure 存储帐户和容器
  必须先创建 Azure 存储帐户和 blob 容器以及共享访问签名, 然后才能开始将 SQL Server 数据文件存储在 Azure 存储中。 第1课逐步讲解登录到 Azure 管理门户、创建存储帐户、blob 容器和共享访问签名的步骤。  
  
 默认情况下，只有存储帐户的所有者可访问该帐户内的 Blob、表和队列。 若要能够使用此项新的 SQL Server 增强在不共享存储帐户访问密钥的情况下访问这些资源，必须执行以下操作：  
  
-   将容器的权限设置为私有。  
  
-   创建共享访问签名。 通过它，可委派对容器、Blob、表或队列资源的受限访问权限，方法为指定间隔，期间这些资源可用，以及客户端将对这些资源拥有的权限。  
  
-   使用存储的访问策略管理容器或其 Blob 的共享访问签名。 存储的访问策略提供针对共享访问签名的另外一种控制措施，还提供一种撤消这些措施的简单方法。  
  
 有关详细信息, 请参阅[管理对 Azure 存储资源的访问](https://msdn.microsoft.com/library/windowsazure/ee393343.aspx)。  
  
## <a name="create-storage-account"></a>创建存储帐户  
 若要在 Azure 管理门户上创建存储帐户, 请执行以下步骤:  
  
1.  使用帐户登录到[Azure 管理门户](https://manage.windowsazure.com)。 如果你没有 Azure 帐户, 请访问[azure 免费试用版](http://www.windowsazure.com/pricing/free-trial/)。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-1.gif "SQL 14 CTP2")  
  
2.  使用分步说明[创建存储帐户](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)。 请注意, 在创建要用于 Azure 中的 SQL Server 数据文件的存储帐户时, 应取消选择或禁用异地复制。 这是因为对于参与地理复制的多个 Blob 无法保证写入顺序。 如果存储帐户经过地理复制，并且需要恢复，则发生损坏。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-2.gif "SQL 14 CTP2")  
  
## <a name="create-a-blob-container"></a>创建 Blob 容器  
 在 Azure 中, 容器提供一组 blob 的分组。 所有 Blob 必须都在一个容器中。 一个存储帐户可含有无限数量的容器，但必须至少有一个容器。 一个容器可以存储无限数量的 Blob。 有关存储大小限制的最新信息, 请参阅[如何在 .net 中使用 Azure Blob 存储服务](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)。  
  
 若要在 Azure 中创建容器, 请执行以下步骤:  
  
1.  登录到[Azure 管理门户](https://manage.windowsazure.com)。  
  
2.  选择存储帐户, 单击 "**容器**" 选项卡, 然后单击屏幕底部的 "**添加容器**", 这将打开一个新的对话框。  
  
3.  输入容器的名称。  
  
4.  选择 "**专用**" 作为 "**访问类型**"。 当你将访问权限设置为 "专用" 时, Azure 帐户所有者只能读取容器和 blob 数据。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-4.gif "SQL 14 CTP2")  
  
> [!NOTE]  
>  若要以编程方式创建容器，还可使用 REST API。 有关详细信息, 请参阅[创建容器](https://msdn.microsoft.com/library/windowsazure/dd179468.aspx)和[Azure 存储服务 REST API 引用](https://msdn.microsoft.com/library/windowsazure/dd179355.aspx)。  
  
 **下一课：**  
  
 [第 2 课.在容器上创建策略并生成共享访问签名&#40;SAS 密钥&#41;](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)  
  
  
