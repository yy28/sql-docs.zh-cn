---
title: 更改系统管理员帐户 (Master Data Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], changing
ms.assetid: cf30312e-4338-49a7-90f0-6e4f7b431ff8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 593e71b63cb4fc6e63c1c087e62f24c37c399e8e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069929"
---
# <a name="change-the-system-administrator-account-master-data-services"></a>更改系统管理员帐户 (Master Data Services)
  你可以指定为的用户帐户[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]系统管理员联系。  
  
> [!WARNING]  
>  当您完成此过程后，将删除旧系统管理员用户帐户。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-   必须将新管理员的用户名添加到[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]的“用户”列表中。 有关详细信息，请参阅[将用户添加&#40;Master Data Services&#41;](add-a-user-master-data-services.md)。  
  
-   您必须有权查看 mdm.tblUser 和在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中执行 mdm.udpSecurityMemberProcessRebuildModel 存储过程。 有关详细信息，请参阅[数据库对象安全性 (Master Data Services)](../../2014/master-data-services/database-object-security-master-data-services.md)。  
  
### <a name="to-change-the-administrator-account"></a>更改管理员帐户  
  
1.  打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 并连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 数据库的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实例。  
  
2.  在 mdm.tblUser 中，找到的用户，将成为新管理员，并复制中的值`SID`列。  
  
3.  创建新查询。  
  
4.  键入以下文本替换*DOMAIN\user_name*具有新管理员的用户名称和*SID*使用在步骤 2 中复制的值。  
  
    ```  
    EXEC [mdm].[udpSecuritySetAdministrator] @UserName='DOMAIN\user_name', @SID = 'SID', @PromoteNonAdmin = 1  
    ```  
  
5.  运行查询。  
  
## <a name="see-also"></a>请参阅  
 [管理员&#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)  
  
  
