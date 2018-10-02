---
title: 测试用户权限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: 83a03b85-ea7f-4b4a-b19b-f7eca534ffae
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 8ddcd6d754ce1b760d91462847b796e4ec8de933
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47594605"
---
# <a name="test-a-user39s-permissions-master-data-services"></a>测试用户权限 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以创建测试用户并登录到 Web 应用程序以测试权限。当某个用户尝试访问 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] URL 时，将会对该用户的凭据进行身份验证。 在 Internet Explorer 中，安全设置控制是否自动进行身份验证，或者用户是否必须输入用户名和密码。 若要更改这些设置，请完成以下步骤：  
  
### <a name="to-test-a-users-security"></a>测试用户的安全设置  
  
1.  在 Internet Explorer 7 和更高版本中，依次单击 **“工具”**、 **“Internet 选项”** 和 **“安全”** 选项卡。  
  
2.  单击 **“本地 Intranet”** ，然后单击 **“自定义级别”** 按钮。  
  
3.  在 **“用户验证”** 部分，选择 **“用户名和密码提示”**。  
  
4.  下次您打开浏览器窗口时，将提示您输入用户名和密码。  
  
## <a name="see-also"></a>另请参阅  
 [安全性 (Master Data Services)](../master-data-services/security-master-data-services.md)  
  
  
