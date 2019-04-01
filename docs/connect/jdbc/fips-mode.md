---
title: 在 JDBC FIPS 模式 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: craigg
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: kenvh
ms.openlocfilehash: 8fb6ea7bf6abfb1f347d0541a01bae91aacf5f1c
ms.sourcegitcommit: 0c049c539ae86264617672936b31d89456d63bb0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58618274"
---
# <a name="fips-mode"></a>FIPS 模式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver for SQL Server 支持在 Jvm 配置为运行*符合 FIPS 140*。

#### <a name="prerequisites"></a>必备条件

- FIPS 配置的 JVM
- 相应的 SSL 证书
- 相应的策略文件
- 相应的配置参数

## <a name="fips-configured-jvm"></a>FIPS 配置的 JVM

通常情况下，应用程序可配置`java.security`文件为使用 FIPS 兼容的加密提供程序。 请参阅特定于有关如何配置 FIPS 140 合规性 JVM 的文档。

若要查看的 FIPS 配置的已批准的模块，请参阅[验证加密模块验证程序中的模块](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules)。

供应商可能有一些附加步骤来配置与 FIPS 的 JVM。

## <a name="appropriate-ssl-certificate"></a>相应的 SSL 证书
若要连接到 SQL Server 在 FIPS 模式下，有效的 SSL 证书是必需的。 安装或将其导入 Java 密钥存储在客户端计算机 (JVM) 上启用了 FIPS。

### <a name="importing-ssl-certificate-in-java-keystore"></a>导入 Java 密钥存储中的 SSL 证书
Fips，很可能需要导入的证书 (.cert) PKCS 或特定于提供程序的格式中。
使用以下代码片段导入 SSL 证书并将其存储在工作目录中具有相应的密钥存储格式。 _信任\_应用商店\_密码_Java 密钥存储的是你的密码。

```java
public void saveGenericKeyStore(
        String provider,
        String trustStoreType,
        String certName,
        String certPath
        ) throws KeyStoreException, CertificateException,
            NoSuchAlgorithmException, NoSuchProviderException,
            IOException
{
    KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
    FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
    ks.load(null, null);
    ks.setCertificateEntry(certName, getCertificate(certPath));
    ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
    os.flush();
    os.close();
}

private Certificate getCertificate(String pathName)
        throws FileNotFoundException, CertificateException
{
    FileInputStream fis = new FileInputStream(pathName);
    CertificateFactory cf = CertificateFactory.getInstance("X.509");
    return cf.generateCertificate(fis);
}
```

下面的示例导入带有 BouncyCastle 提供程序 PKCS12 格式的 Azure SSL 证书。 在名为的工作目录中导入证书_MyTrustStore\_PKCS12_通过使用以下代码片段：

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>相应的策略文件
对于 FIPS 某些提供程序，需要使用不受限制的策略 jar。 在这种情况下，sun / Oracle 下载 Java Cryptography Extension (JCE) 不受限制 Strength Jurisdiction Policy Files 有关[JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)或[JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)。 

## <a name="appropriate-configuration-parameters"></a>相应的配置参数
若要在与 FIPS 兼容模式下运行 JDBC 驱动程序，请配置连接属性下, 表中所示。 

#### <a name="properties"></a>属性 

|属性|类型|，则“默认”|描述|说明|
|---|---|---|---|---|
|encrypt|布尔 [“true / false”]|“false”|启用 FIPS 的 JVM 加密属性应为 **，则返回 true**||
|TrustServerCertificate|布尔 [“true / false”]|“false”|Fips，用户需要验证证书链，因此，用户应使用 **"false"** 此属性的值。 ||
|trustStore|String|null|您可以导入你的证书为 Java 密钥存储文件路径。 如果您的系统，则无需传递任何内容安装证书。 驱动程序使用 cacerts 或 jssecacerts 文件。||
|trustStorePassword|String|null|用于检查 trustStore 数据完整性的密码。||
|fips|布尔 [“true / false”]|“false”|启用 FIPS 的 JVM 此属性应为 **，则返回 true**|添加在 6.1.4 (稳定版本 6.2.2)||
|fipsProvider|String|null|JVM 中配置的 FIPS 提供程序。 例如，BCFIPS 或 SunPKCS11 NSS |6.1.2 中添加 (稳定版本 6.2.2)，已弃用在 6.4.0-请参阅详细信息[此处](https://github.com/Microsoft/mssql-jdbc/pull/460)。|
|trustStoreType|String|JKS|FIPS 模式下将信任存储区类型设置为 PKCS12 或类型由 FIPS 提供程序定义 |6.1.2 中添加 (稳定版本 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
