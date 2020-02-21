---
title: 演示将 Azure Key Vault 提供程序与 Always Encrypted 配合使用的示例 | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: fca498fbc7f79dcfc8852799ade6e230952ea082
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75250957"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted"></a>演示将 Azure Key Vault 提供程序与 Always Encrypted 配合使用的示例

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

此示例演示在访问加密列时，如何使用 Azure Key Vault 提供程序。

[!code-csharp [AKVProvider Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderExample.cs#1)]

## <a name="see-also"></a>另请参阅

- [演示将 Azure Key Vault 提供程序与通过安全 Enclaves 启用的 Always Encrypted 配合使用的示例](azure-key-vault-enclave-example.md)
- [教程：使用具有安全 enclave 的 Always Encrypted 开发 .NET 应用程序](tutorial-always-encrypted-enclaves-develop-net-apps.md)
- [对用于 SQL Server 的 Microsoft .NET 数据提供程序使用 Always Encrypted](sqlclient-support-always-encrypted.md)
