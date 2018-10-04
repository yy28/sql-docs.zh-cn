---
title: 第 1 课： 创建 Windows Azure 存储对象 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 74edd1fd-ab00-46f7-9e29-7ba3f1a446c5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 26ab900e8a043399191e8c26314d47e48dd3e1a8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137377"
---
# <a name="lesson-1-create-windows-azure-storage-objects"></a>第 1 课：创建 Windows Azure 存储对象
  在云存储中创建 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份之前，必须先创建存储帐户，然后再创建 Blob 容器。 第 1 课将指导您完成登录 Windows Azure 管理门户以创建存储帐户和 Blob 容器的步骤。  
  
## <a name="create-a-storage-account"></a>创建存储帐户  
 若要从 Windows Azure 管理门户创建存储帐户，请使用以下步骤：  
  
1.  使用您的帐户登录 Windows Azure 管理门户。 如果您没有 Windows Azure 帐户[请访问 Windows Azure 3 个月免费试用版](http://go.microsoft.com/fwlink/?LinkId=271927)。  
  
     ![Windows Azure 登录屏幕](../../2014/tutorials/media/windowazurelogin-backuptocloud.gif "Windows Azure 登录屏幕")  
  
2.  使用详细的分步说明[此处](http://go.microsoft.com/fwlink/?LinkId=271926)，以创建存储帐户。  
  
3.  浏览到您在上一步中创建的存储帐户。 从 web 页的底部中心，单击**管理密钥**。 此时将显示帐户信息。 复制存储帐户名和访问键。 创建 SQL 存储凭据时需要此信息。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用此信息来访问存储帐户并创建备份。  
  
     ![Windows Azure 存储帐户密钥的屏幕截图](../../2014/tutorials/media/manageaccesskeys-backuptocloud.gif "Windows Azure 存储帐户密钥的屏幕截图")  
  
    > [!NOTE]  
    >  还可以使用 REST API 以编程方式创建存储帐户。 有关详细信息，请参阅[创建存储帐户](http://go.microsoft.com/fwlink/?LinkId=271928)。  
  
### <a name="create-a-blob-container"></a>创建 Blob 容器  
 容器提供了一组 blob 的分组。 所有 Blob 必须都在一个容器中。 一个帐户可以包含无限数量的容器，但必须至少具有一个容器。 一个容器可以存储无限数量的 Blob。  
  
 若要创建容器，请使用以下步骤：  
  
1.  选择存储帐户中，单击**容器**选项卡，单击**添加容器**这将打开新建对话框的屏幕底部。  
  
     ![在管理门户中创建一个容器](../../2014/tutorials/media/backuptocloud.gif "在管理门户中创建容器")  
  
2.  输入容器的名称。 记下您指定的容器名称。 此信息用在第 3 课和第 4 课的 T-SQL 语句的 URL（备份文件的路径）中。  
  
3.  选择专用的**访问类型**。 为了保护备份文件的安全，建议您创建专用容器。  
  
     ![创建新的 blob 容器](../../2014/tutorials/media/backuptocloud-newblobcontainer.gif "创建新的 blob 容器")  
  
    > [!NOTE]  
    >  即使您选择创建公共容器，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份和还原仍需要对存储帐户进行身份验证。  
    >   
    >  还可以使用 REST API 以编程方式创建容器。 有关详细信息，请参阅[创建容器](http://go.microsoft.com/fwlink/?LinkId=271946)。  
  
### <a name="next-lesson"></a>下一课  
 [第 2 课： 创建 SQL Server 凭据](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md)。  
  
  
