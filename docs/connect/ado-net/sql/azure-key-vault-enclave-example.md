---
title: 展示如何结合使用 Azure Key Vault 提供程序和已启用安全 Enclave 的 Always Encrypted 的示例 | Microsoft Docs
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
ms.openlocfilehash: a4ba44733d2a14323f128f1ab105e79169b90cce
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75250946"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted-enabled-with-secure-enclaves"></a>展示如何结合使用 Azure Key Vault 提供程序和已启用安全 Enclave 的 Always Encrypted 的示例

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

此示例展示了如何在访问加密列时使用 Azure Key Vault 提供程序。

[!code-csharp [Azure Key Vault Provider with Enclave Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderWithEnclaveProviderExample.cs#1)]

## <a name="see-also"></a>另请参阅

- [展示结合使用 Azure Key Vault 提供程序和 Always Encrypted 的示例](azure-key-vault-example.md)
- [教程：使用具有安全 enclave 的 Always Encrypted 开发 .NET 应用程序](tutorial-always-encrypted-enclaves-develop-net-apps.md)
- [结合 Always Encrypted 和 Microsoft .NET Data Provider for SQL Server](sqlclient-support-always-encrypted.md)
