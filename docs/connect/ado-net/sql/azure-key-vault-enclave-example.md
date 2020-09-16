---
description: 展示如何结合使用 Azure Key Vault 提供程序和已启用安全 Enclave 的 Always Encrypted 的示例
title: 展示如何结合使用 Azure Key Vault 提供程序和已启用安全 Enclave 的 Always Encrypted 的示例 | Microsoft Docs
ms.custom: ''
ms.date: 07/09/2020
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: 1cb8669a14039f7155e6c31fce62de44c1fac03a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438639"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted-enabled-with-secure-enclaves"></a>展示如何结合使用 Azure Key Vault 提供程序和已启用安全 Enclave 的 Always Encrypted 的示例

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

此示例展示了如何在访问加密列时使用 Azure Key Vault 提供程序。

[!code-csharp [Azure Key Vault Provider with Enclave Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderWithEnclaveProviderExample.cs#1)]

> [!NOTE]
> 具有安全 Enclave 的 Always Encrypted 仅支持在 Windows 上使用。

## <a name="see-also"></a>另请参阅

- [展示结合使用 Azure Key Vault 提供程序和 Always Encrypted 的示例](azure-key-vault-example.md)
- [教程：使用具有安全 enclave 的 Always Encrypted 开发 .NET 应用程序](tutorial-always-encrypted-enclaves-develop-net-apps.md)
- [结合 Always Encrypted 和 Microsoft .NET Data Provider for SQL Server](sqlclient-support-always-encrypted.md)
