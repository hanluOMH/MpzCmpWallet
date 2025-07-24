This is a Compose Multiplatform project targeting Android, iOS.

It's a minimal example of how to write a wallet app supporting ISO mdoc proximity presentment
according to ISO/IEC 18013-5:2021, using QR code as engagement.

Learn more about [Multipaz](https://github.com/openwallet-foundation-labs/identity-credential)…

Learn more about [Compose Multiplatform](https://www.jetbrains.com/compose-multiplatform/)…

Learn more about [Kotlin Multiplatform](https://kotlinlang.org/docs/multiplatform.html)…

This is not an official or supported Google product.

About to how let Reader to recognize the issuer(trust issuer)
[Hanlu] use david’s method(https://discord.com/channels/1022962884864643214/1179828955717574707/1397695583879430164),reader app can recognize issuer
https://github.com/hanluOMH/MpzCmpWallet/blob/529aa6de1be77f58d473d18758b826080e980917/composeApp/src/commonMain/kotlin/org/multipaz/samples/wallet/cmp/App.kt#L116,
`println("IACA cert: ${iacaCert.toPem()}"), load pem to reader app, then reader app will add this issuer to trust list.

Because currently app dynamically generate cert, use below method can gnereate a constant cert:
ran multipazctl generateIaca 
         #Creates:
        #iaca_private_key.pem → used for signing credentials (in the Holder App)
        #iaca_certificate.pem → contains the public key (used in the Verifier App)
copied the iaca_certificate.pem to the iacaCert variable
generatd the public key for iaca_private_key.pem using the following command
openssl pkey -in iaca_private_key.pem -pubout -out iaca_public_key.pem
created an EcPublicKey using iaca_public_key.pem
        #Same public key as inside the certificate(imported from by the reader or verifer app)
created EcPrivateKey using iaca_private_key.pem and the EcPublicKey from the previous step
        # is used for signing credentials (in the Holder App)
copied the iaca_certificate.pem to the reader app, scanned QR & it works!

#dsCert is used to verify document(not credential),Document Signing Certificate

#readerTrustManager used by holder app to verify  reader(verifier) identity