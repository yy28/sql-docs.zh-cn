---
title: Azure Data Lake Analytics 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.prod_service: integration-services
ms.component: connection-manager
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 7
author: yanancai
ms.author: yanacai
manager: craigg
ms.openlocfilehash: 17b63aad55cf50262d7e1e56267859b1a34cc9d3
ms.sourcegitcommit: 44e9bf62f2c75449c17753ed66bf85c43928dbd5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37854400"
---
# <a name="azure-data-lake-analytics-connection-manager"></a>Azure Data Lake Analytics 连接管理器

SQL Server Integration Services (SSIS) 包可通过下列两种身份验证类型之一使用 Azure Data Lake Analytics 连接管理器连接 Azure Data Lake Analytics 帐户：
-   Azure AD 用户标识
-   Azure AD 服务标识 

Azure Data Lake Analytics 连接管理器是[适用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)的组件。
 
## <a name="configure-the-azure-data-lake-analytics-connection-manager"></a>配置 Azure Data Lake Analytics 连接管理器

1.  在“添加 SSIS 连接管理器” 对话框中，选择“AzureDataLakeAnalytics”，然后选择“添加”。 此时将打开“Azure Data Lake Analytics 连接管理器编辑器”对话框。
  
2.  在“Azure Data Lake Analytics 连接管理器编辑器”对话框的“ADLA 帐户名称”字段中提供 Azure Data Lake Analytics 帐户名称。 例如：myadlaaccountname。
  
3.  在“身份验证”字段中，选择合适的身份验证类型来访问 Azure Data Lake Analytics 中的数据。

    1.  如果选择“Azure AD 用户标识” 身份验证选项，请执行以下操作：
        1. 为“用户名”和“密码”字段提供相应的值。 
    
        2. 选择“测试连接”以测试连接。 如果你或租户管理员以前未允许 SSIS 访问你的 Azure Data Lake Analytics 帐户，请在出现提示时选择“接受”。 若要深入了解此同意体验，请参阅 [Integrating applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications#updating-an-application)（将应用程序与 Azure Active Directory 集成）。
    
        >   [!NOTE] 
        > 如果选择了“Azure AD 用户标识”身份验证选项，则不支持多重身份验证和 Microsoft 帐户身份验证。
    
    2. 如果选择“Azure AD 服务标识” 身份验证选项，请执行以下操作：
        1. 创建 Azure Active Directory (AAD) 应用程序和服务主体，用于访问 Azure Data Lake Analytics 帐户。 若要深入此身份验证选项，请参阅 [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)（使用门户创建可访问资源的 Active Directory 应用程序和服务主体）。
    
        2. 分配相应权限，让此 AAD 应用程序能够访问 Azure Data Lake Analytics 帐户。 了解如何[使用添加用户向导](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-manage-use-portal#add-a-new-user)向 Azure Data Lake Analytics 帐户授予权限。 
    
        3. 提供“应用程序 ID”、“身份验证密钥”和“租户 ID”字段的值。
    
        4. 选择“测试连接”以测试连接。  

4.  选择“确定”以关闭“Azure Data Lake Analytics 连接管理器编辑器”对话框。  

## <a name="view-the-properties-of-the-connection-manager"></a>查看连接管理器的属性
你可以看到你在“属性”  窗口中创建的连接管理器的属性。  
  
  
