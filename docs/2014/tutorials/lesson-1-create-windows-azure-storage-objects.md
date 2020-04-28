---
title: 第1课：创建 Azure 存储对象 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 74edd1fd-ab00-46f7-9e29-7ba3f1a446c5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 53fcba3401a6798fb865613470ba78aa05e9b6dd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "70176107"
---
# <a name="lesson-1-create-azure-storage-objects"></a>第 1 课：创建 Azure 存储对象
  在云存储中创建 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份之前，必须先创建存储帐户，然后再创建 Blob 容器。 第1课将指导你完成登录 Azure 管理门户、创建存储帐户和 blob 容器的步骤。  
  
## <a name="create-a-storage-account"></a>创建存储帐户  
 若要从 Azure 管理门户创建存储帐户，请使用以下步骤：  
  
1.  使用你的帐户登录到 Azure 管理门户。 如果你没有 Azure 帐户，请[访问 azure 3 个月免费试用版](https://go.microsoft.com/fwlink/?LinkId=271927)。  
  
     ![Azure 登录屏幕](../../2014/tutorials/media/windowazurelogin-backuptocloud.gif "Azure 登录屏幕")  
  
2.  使用[此处](https://go.microsoft.com/fwlink/?LinkId=271926)详细介绍的分步说明创建存储帐户。  
  
3.  浏览到您在上一步中创建的存储帐户。 单击网页底部的 "**管理密钥**"。 此时将显示帐户信息。 复制存储帐户名和访问键。 创建 SQL 存储凭据时需要此信息。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用此信息来访问存储帐户并创建备份。  
  
     ![Azure 存储帐户密钥的屏幕截图](../../2014/tutorials/media/manageaccesskeys-backuptocloud.gif "Azure 存储帐户密钥的屏幕截图")  
  
    > [!NOTE]  
    >  还可以使用 REST API 以编程方式创建存储帐户。 有关详细信息，请参阅[创建存储帐户](https://go.microsoft.com/fwlink/?LinkId=271928)。  
  
### <a name="create-a-blob-container"></a>创建 Blob 容器  
 容器对 Blob 集进行分组。 所有 Blob 必须都在一个容器中。 一个帐户可以包含无限数量的容器，但必须至少具有一个容器。 一个容器可以存储无限数量的 Blob。  
  
 若要创建容器，请使用以下步骤：  
  
1.  选择存储帐户，单击 "**容器**" 选项卡，然后单击屏幕底部的 "**添加容器**"，这将打开一个新的对话框。  
  
     ![在管理门户中创建容器](../../2014/tutorials/media/backuptocloud.gif "在管理门户中创建容器")  
  
2.  输入容器的名称。 记下您指定的容器名称。 此信息用在第 3 课和第 4 课的 T-SQL 语句的 URL（备份文件的路径）中。  
  
3.  选择 "专用" 作为 "**访问类型**"。 为了保护备份文件的安全，建议您创建专用容器。  
  
     ![正在创建新的 Blob 容器。](../../2014/tutorials/media/backuptocloud-newblobcontainer.gif "正在创建新的 Blob 容器。")  
  
    > [!NOTE]  
    >  即使您选择创建公共容器，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份和还原仍需要对存储帐户进行身份验证。  
    >   
    >  还可以使用 REST API 以编程方式创建容器。 有关详细信息，请参阅[创建容器](https://go.microsoft.com/fwlink/?LinkId=271946)。  
  
### <a name="next-lesson"></a>下一课  
 [第2课：创建 SQL Server 凭据](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md)。  
  
  
