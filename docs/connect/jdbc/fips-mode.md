---
title: JDBC 中的 FIPS 模式 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
manager: kenvh
ms.openlocfilehash: 63681ee474d4993e248bf02dcabd9065317ffa39
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028057"
---
# <a name="fips-mode"></a>FIPS 模式

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver for SQL Server 支持在配置为“符合 FIPS 140 标准”的 JVM 中运行。

#### <a name="prerequisites"></a>必备条件

- 配置了 FIPS 的 JVM
- 相应的 SSL 证书
- 相应的策略文件
- 相应的配置参数

## <a name="fips-configured-jvm"></a>配置了 FIPS 的 JVM

通常，应用程序可以将 `java.security` 文件配置为使用符合 FIPS 标准的加密提供程序。 有关如何配置符合 FIPS 140 标准的信息，请参阅特定于 JVM 的文档。

若要查看已批准的 FIPS 配置模块，请参阅[加密模块验证计划中的已验证模块](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules)。

供应商可能有一些其他步骤来配置启用了 FIPS 的 JVM。

## <a name="appropriate-ssl-certificate"></a>相应的 SSL 证书
为了连接到 FIPS 模式下的 SQL Server，需要有效的 SSL 证书。 将其安装或导入到启用了 FIPS 的客户端计算机 (JVM) 上的 Java 密钥存储中。

### <a name="importing-ssl-certificate-in-java-keystore"></a>将 SSL 证书导入到 Java 密钥存储中
对于 FIPS，很可能需要导入 PKCS 格式或特定于提供程序的格式的证书 (.cert)。
使用以下代码片段导入 SSL 证书，并使用相应的密钥存储格式将其存储在工作目录中。 _TRUST\_STORE\_PASSWORD_ 是 Java 密钥存储的密码。

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

以下示例使用 BouncyCastle 提供程序导入 PKCS12 格式的 Azure SSL 证书。 该证书使用以下代码片段导入到名为 _MyTrustStore\_PKCS12_ 的工作目录中：

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>相应的策略文件
对于某些 FIPS 提供程序，需要无限制的策略 jar。 在这些情况下，对于 Sun/Oracle，下载适用于 [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) 或 [JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html) 的 Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files。 

## <a name="appropriate-configuration-parameters"></a>相应的配置参数
若要在符合 FIPS 标准的模式下运行 JDBC 驱动程序，请按下表中所示配置连接属性。 

#### <a name="properties"></a>属性 

|properties|类型|默认|说明|说明|
|---|---|---|---|---|
|encrypt|布尔 [“true / false”]|“false”|对于启用了 FIPS 的 JVM，加密属性应为 true||
|TrustServerCertificate|布尔 [“true / false”]|“false”|对于 FIPS，用户需要验证证书链，因此用户应将“false”值用于此属性。 ||
|trustStore|String|Null|导入证书的 Java 密钥存储文件路径。 如果在系统上安装证书，则无需传递任何内容。 驱动程序使用 cacerts 或 jssecacerts 文件。||
|trustStorePassword|String|Null|用于检查 trustStore 数据完整性的密码。||
|fips|布尔 [“true / false”]|“false”|对于启用了 FIPS 的 JVM，此属性应为 true|已在 6.1.4 中添加（稳定版 6.2.2）||
|fipsProvider|String|Null|JVM 中配置的 FIPS 提供程序。 例如，BCFIPS 或 SunPKCS11-NSS |已在 6.1.2 中添加（稳定版 6.2.2），已在 6.4.0 中弃用 - 请在[此处](https://github.com/Microsoft/mssql-jdbc/pull/460)查看详细信息。|
|trustStoreType|String|JKS|对于 FIPS 模式，请将信任存储类型设置为 PKCS12 或由 FIPS 提供程序定义的类型 |已在 6.1.2 中添加（稳定版 6.2.2）||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
