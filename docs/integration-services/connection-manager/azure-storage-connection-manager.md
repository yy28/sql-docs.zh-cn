---
title: Azure 存储连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f171499471f8f94ad970446d31cf796f4ab55fb7
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028773"
---
# <a name="azure-storage-connection-manager"></a>Azure 存储连接管理器

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  通过 Azure 存储连接管理器，SSIS 包可与 Azure 存储帐户进行连接  。
   
 Azure 存储连接管理器是[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)的一个组件  。 
  
在“添加 SSIS 连接管理器”  对话框中，选择“AzureStorage”  ，然后单击“添加”  。  
  
可使用以下属性。

- **服务：** 指定要连接到的存储服务。
- **帐户名：** 指定存储帐户名。
- **身份验证：** 指定要使用的身份验证方法。 支持 AccessKey 和 ServicePrincipal 身份验证   。
    - **AccessKey：** 指定此身份验证方法的帐户密钥  。
    - **ServicePrincipal：** 对于此身份验证方法，请指定服务主体的应用程序 ID、应用程序密钥和租户 ID    。
      要使“测试连接”起作用，应向服务主体分配至少存储帐户的“存储 Blob 数据读取器”角色   。
      请参阅[此](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal)页获取详细信息。
- **环境：** 指定托管存储帐户的云环境。

## <a name="managed-identities-for-azure-resources-authentication"></a>Azure 资源身份验证的托管标识
在 [Azure 数据工厂中的 Azure-SSIS 集成运行时](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime)上运行 SSIS 包时，可以使用与数据工厂关联的[托管标识](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity)进行 Azure 存储身份验证。 指定的工厂可以使用此标识访问存储帐户数据，或从/向存储帐户复制数据。

有关 Azure 存储身份验证的常规信息，请参阅[使用 Azure Active Directory 验证对 Azure 存储的访问权限](https://docs.microsoft.com/azure/storage/common/storage-auth-aad)。 若要对 Azure 存储使用托管标识身份验证，请按照以下步骤操作来配置存储帐户：

1. [从 Azure 门户中查找数据工厂托管标识](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)  。 转到数据工厂的“属性”  。 复制“托管标识应用程序 ID”（非托管标识对象 ID）   。

1. **在存储帐户中向托管标识授予适当权限**。 如需了解角色的更多详情，请参阅[使用 RBAC 管理对 Azure 存储数据的访问权限](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal)。

    - 作为源  ，在访问控制 (IAM) 中，至少授予“存储 Blob 数据读取者”  角色。
    - 作为目标  ，在访问控制 (IAM) 中，至少授予“存储 Blob 数据参与者”  角色。

然后，为 Azure 存储连接管理器配置托管标识身份验证  。 完成此操作的方法有两种。

1. 在设计时进行配置。 在 SSIS 设计器中，双击 Azure 存储连接管理器以打开“Azure 存储连接管理器编辑器”  ，再选中“使用托管标识在 Azure 上进行身份验证”  。
    > [!NOTE]
    >  目前，当你在 SSIS 设计器或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 中运行 SSIS 包时，此选项不生效（表明托管标识身份验证不起作用）。
    
1. 在运行时进行配置。 通过 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) 或 [Azure 数据工厂执行 SSIS 包活动](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)执行包时，找到 Azure 存储连接管理器，并将它的属性“ConnectUsingManagedIdentity”  更新为“True”  。
    > [!NOTE]
    >  在 Azure-SSIS 集成运行时中，当托管标识身份验证用于存储操作时，Azure 存储连接管理器上预配的其他所有身份验证方法（例如，访问密钥、服务主体）都会被重写  。

> [!NOTE]
>  若要在现有包上配置托管标识身份验证，首选方法是至少使用[最新 SSIS 设计器](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)重新生成一次 SSIS 项目，然后将此 SSIS 项目重新部署到 Azure-SSIS 集成运行时，这样新的连接管理器属性 ConnectUsingManagedIdentity  才会自动添加到 SSIS 项目中的所有 Azure 存储连接管理器。 另一种方法是，直接在运行时结合使用属性重写和属性路径 \Package.Connections[{连接管理器名称}].Properties[ConnectUsingManagedIdentity]  。

## <a name="see-also"></a>另请参阅  
 [Integration Services (SSIS) 连接](../../integration-services/connection-manager/integration-services-ssis-connections.md)
