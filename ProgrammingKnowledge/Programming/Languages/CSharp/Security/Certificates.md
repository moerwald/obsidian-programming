
In [[CSharp]] kann man selbst signierte Zertifikate via folgenden Code erzeugen:

```CSharp
        private static X509Certificate2 CreateCertificate(DateTimeOffset notBefore, DateTimeOffset notAfter)
        {
            var key = new RSACryptoServiceProvider(2048);
            var certRequest = new CertificateRequest("CN=Test Certificate", key, HashAlgorithmName.SHA256, RSASignaturePadding.Pkcs1);
            certRequest.CertificateExtensions.Add(new X509KeyUsageExtension(X509KeyUsageFlags.DigitalSignature, false));

            var certificate = certRequest.CreateSelfSigned(notBefore, notAfter);
            return new X509Certificate2(certificate.Export(X509ContentType.Pfx));
        }

        private static X509Certificate2 CreateExpiredCertificate()
            => CreateCertificate(DateTimeOffset.UtcNow.AddDays(-365), DateTimeOffset.UtcNow.AddDays(-1));

        private static X509Chain CreateChainWithFakedCertificate(X509Certificate2 certificate)
        {
            var chain = new X509Chain();
            chain.ChainPolicy.ExtraStore.Add(certificate);
            chain.ChainPolicy.VerificationFlags = X509VerificationFlags.AllowUnknownCertificateAuthority;
            chain.Build(certificate);
            return chain;
        }



```

#Zertifikate
#CSharp 