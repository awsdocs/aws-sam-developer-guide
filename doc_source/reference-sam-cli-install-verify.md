# Verify the integrity of the AWS SAM CLI installer<a name="reference-sam-cli-install-verify"></a>

When installing the AWS Serverless Application Model Command Line Interface \(AWS SAM CLI\) using a package installer, you can verify its integrity before installation\. This is an optional, but highly recommended step\.

The two options of verification available to you are:
+ Verify the package installer signature file\.
+ Verify the package installer hash value\.

When available for your platform, we recommend verifying the signature file option\. This option offers an extra layer of security since the key values are published here and managed separately from our GitHub repository\.

**Topics**
+ [Verify the installer signature file](#reference-sam-cli-install-verify-signature)
+ [Verify the hash value](#reference-sam-cli-install-verify-hash)

## Verify the installer signature file<a name="reference-sam-cli-install-verify-signature"></a>

### Linux<a name="reference-sam-cli-install-verify-signature-linux"></a>

#### x86\_64 \- command line installer<a name="reference-sam-cli-install-verify-signature-linux-x8664"></a>

AWS SAM uses [GnuPG](https://www.gnupg.org/) to sign the AWS SAM CLI \.zip installer\. Verification is performed in the following steps:

1. Use the primary public key to verify the signer public key\.

1. Use the signer public key to verify the AWS SAM CLI package installer\.

**To verify the integrity of the signer public key**

1. Copy the primary public key and save it to your local machine as a `.txt` file\. For example, *`primary-public-key.txt`*\.

   ```
   -----BEGIN PGP PUBLIC KEY BLOCK-----
   Version: GnuPG v2.0.22 (GNU/Linux)
   
   mQINBGRuSzMBEADsqiwOy78w7F4+sshaMFRIwRGNRm94p5Qey2KMZBxekFtoryVD
   D9jEOnvupx4tvhfBHz5EcUHCEOdl4MTqdBy6vVAshozgxVb9RE8JpECn5lw7XC69
   4Y7Gy1TKKQMEWtDXElkGxIFdUWvWjSnPlzfnoXwQYGeE93CUS3h5dImP22Yk1Ct6
   eGGhlcbg1X4L8EpFMj7GvcsU8f7ziVI/PyC1Xwy39Q8/I67ip5eU5ddxO/xHqrbL
   YC7+8pJPbRMej2twT2LrcpWWYAbprMtRoa6WfE0/thoo3xhHpIMHdPfAA86ZNGIN
   kRLjGUg7jnPTRW4Oin3pCc8nT4Tfc1QERkHm641gTC/jUvpmQsM6h/FUVP2i5iE/
   JHpJcMuL2Mg6zDo3x+3gTCf+Wqz3rZzxB+wQT3yryZs6efcQy7nROiRxYBxCSXX0
   2cNYzsYLb/bYaW8yqWIHD5IqKhw269gp2E5Khs60zgS3CorMb5/xHgXjUCVgcu8a
   a8ncdf9fjl3WS5p0ohetPbO2ZjWv+MaqrZOmUIgKbA4RpWZ/fU97P5BW9ylwmIDB
   sWy0cMxg8MlvSdLytPieogaM0qMg3u5qXRGBr6Wmevkty0qgnmpGGc5zPiUbtOE8
   CnFFqyxBpj5IOnG0KZGVihvn+iRxrv6GO7WWO92+Dc6m94U0EEiBR7QiOwARAQAB
   tDRBV1MgU0FNIENMSSBQcmltYXJ5IDxhd3Mtc2FtLWNsaS1wcmltYXJ5QGFtYXpv
   bi5jb20+iQI/BBMBCQApBQJkbkszAhsvBQkHhM4ABwsJCAcDAgEGFQgCCQoLBBYC
   AwECHgECF4AACgkQQv1fenOtiFqTuhAAzi5+ju5UVOWqHKevOJSO08T4QB8HcqAE
   SVO3mY6/j29knkcL8ubZP/DbpV7QpHPI2PB5qSXsiDTP3IYPbeY78zHSDjljaIK3
   njJLMScFeGPyfPpwMsuY4nzrRIgAtXShPA8N/k4ZJcafnpNqKj7QnPxiC1KaIQWm
   pOtvb8msUF3/s0UTa5Ys/lNRhVC0eGg32ogXGdojZA2kHZWdm9udLo4CDrDcrQT7
   NtDcJASapXSQL63XfAS3snEc4e1941YxcjfYZ33rel8K9juyDZfi1slWR/L3AviI
   QFIaqSHzyOtP1oinUkoVwL8ThevKD3Ag9CZflZLzNCV7yqlF8RlhEZ4zcE/3s9El
   WzCFsozb5HfE1AZonmrDh3SyOEIBMcS6vG5dWnvJrAuSYv2rX38++K5Pr/MIAfOX
   DOI1rtA+XDsHNv9lSwSy0lt+iClawZANO9IXCiN1rOYcVQlwzDFwCNWDgkwdOqS0
   gOA2f8NF9lE5nBbeEuYquoOl1Vy8+ICbgOFs9LoWZlnVh7/RyY6ssowiU9vGUnHI
   L8f9jqRspIz/Fm3JD86ntZxLVGkeZUz62FqErdohYfkFIVcv7GONTEyrz5HLlnpv
   FJ0MR0HjrMrZrnOVZnwBKhpbLocTsH+3t5It4ReYEX0f1DIOL/KRwPvjMvBVkXY5
   hblRVDQoOWc=
   =d9oG
   -----END PGP PUBLIC KEY BLOCK-----
   ```

1. Import the primary public key to your keyring\.

   ```
   $ gpg --import primary-public-key.txt
   							
   gpg: directory `/home/.../.gnupg' created
   gpg: new configuration file `/home/.../.gnupg/gpg.conf' created
   gpg: WARNING: options in `/home/.../.gnupg/gpg.conf' are not yet active during this run
   gpg: keyring `/home/.../.gnupg/secring.gpg' created
   gpg: keyring `/home/.../.gnupg/pubring.gpg' created
   gpg: /home/.../.gnupg/trustdb.gpg: trustdb created
   gpg: key 73AD885A: public key "AWS SAM CLI Primary <aws-sam-cli-primary@amazon.com>" imported
   gpg: Total number processed: 1
   gpg:               imported: 1  (RSA: 1)
   ```

1. Copy the signer public key and save it to your local machine as a `.txt` file\. For example, *`signer-public-key.txt`*\.

   ```
   -----BEGIN PGP PUBLIC KEY BLOCK-----
   Version: GnuPG v2.0.22 (GNU/Linux)
   
   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
   GXwoX75FwIEHA3n5Q7rZ69Ea6Q==
   =ZIO7
   -----END PGP PUBLIC KEY BLOCK-----
   ```

1. Import the signer public key to your keyring\.

   ```
   $ gpg --import signer-public-key.txt
   							
   gpg: key FE0ADDFA: public key "AWS SAM CLI Team <aws-sam-cli-signer@amazon.com>" imported
   gpg: Total number processed: 1
   gpg:               imported: 1  (RSA: 1)
   gpg: no ultimately trusted keys found
   ```

   Take note of the key value from the output\. For example, *`FE0ADDFA`*\.

1. Use the key value to obtain and verify the signer public key fingerprint\.

   ```
   $ gpg --fingerprint FE0ADDFA
   							
   pub   4096R/FE0ADDFA 2023-05-23 [expires: 2025-05-22]
         Key fingerprint = 37D8 BE16 0355 2DA7 BD6A  04D8 C7A0 5F43 FE0A DDFA
   uid                  AWS SAM CLI Team <aws-sam-cli-signer@amazon.com>
   ```

   The fingerprint should match the following:

   ```
   37D8 BE16 0355 2DA7 BD6A  04D8 C7A0 5F43 FE0A DDFA
   ```

   If the fingerprint string doesn’t match, do not use the AWS SAM CLI installer\. Escalate to the AWS SAM team by [creating an issue](https://github.com/aws/aws-sam-cli/issues/new?assignees=&labels=stage%2Fneeds-triage&projects=&template=Bug_report.md&title=Bug%3A+TITLE) in the *aws\-sam\-cli GitHub repository*\.

1. Verify the signatures of the signer public key:

   ```
   $ gpg --check-sigs FE0ADDFA
   							
   pub   4096R/FE0ADDFA 2023-05-23 [expires: 2025-05-22]
   uid                  AWS SAM CLI Team <aws-sam-cli-signer@amazon.com>
   sig!3        FE0ADDFA 2023-05-23  AWS SAM CLI Team <aws-sam-cli-signer@amazon.com>
   sig!         73AD885A 2023-05-24  AWS SAM CLI Primary <aws-sam-cli-primary@amazon.com>
   ```

   If you see `1 signature not checked due to a missing key`, repeat the previous steps to import the primary and signer public keys to your keyring\.

   You should see the key values for both the primary public key and signer public key listed\.

Now that you have verified the integrity of the signer public key, you can use the signer public key to verify the AWS SAM CLI package installer\.

**To verify the integrity of the AWS SAM CLI package installer**

1. **Obtain the AWS SAM CLI package signature file** – Download the signature file for the AWS SAM CLI package installer by using the following command:

   ```
   $ wget https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-linux-x86_64.zip.sig
   ```

1. **Verify the signature file** – Pass both the downloaded `.sig` and `.zip` files as parameters to the `gpg` command\. The following is an example:

   ```
   $ gpg --verify aws-sam-cli-linux-x86_64.zip.sig aws-sam-cli-linux-x86_64.zip
   ```

   The output should look similar to the following:

   ```
   gpg: Signature made Tue 30 May 2023 10:03:57 AM UTC using RSA key ID FE0ADDFA
   gpg: Good signature from "AWS SAM CLI Team <aws-sam-cli-signer@amazon.com>"
   gpg: WARNING: This key is not certified with a trusted signature!
   gpg:          There is no indication that the signature belongs to the owner.
   Primary key fingerprint: 37D8 BE16 0355 2DA7 BD6A  04D8 C7A0 5F43 FE0A DDFA
   ```
   + The `WARNING: This key is not certified with a trusted signature!` message can be ignored\. It occurs because there isn’t a chain of trust between your personal PGP key \(if you have one\) and the AWS SAM CLI PGP key\. For more information, see [ Web of trust](https://en.wikipedia.org/wiki/Web_of_trust)\.
   + If the output contains the phrase `BAD signature`, check that you performed the procedure correctly\. If you continue to get this response, escalate to the AWS SAM team by [creating an issue](https://github.com/aws/aws-sam-cli/issues/new?assignees=&labels=stage%2Fneeds-triage&projects=&template=Bug_report.md&title=Bug%3A+TITLE) in the *aws\-sam\-cli GitHub repository* and avoid using the downloaded file\.

   The `Good signature from "AWS SAM CLI Team <aws-sam-cli-signer@amazon.com>"` message means that the signature is verified and you can move forward with installation\.

### macOS<a name="reference-sam-cli-install-verify-signature-macos"></a>

#### GUI and command line installer<a name="reference-sam-cli-install-verify-signature-macos-installer"></a>

You can verify the integrity of the AWS SAM CLI package installer signature file by using the `pkgutil` tool or manually\.

**To verify using pkgutil**

1. Run the following command, providing the path to the downloaded installer on your local machine:

   ```
   $ pkgutil --check-signature /path/to/aws-sam-cli-installer.pkg
   ```

   The following is an example:

   ```
   $ pkgutil --check-signature /Users/user/Downloads/aws-sam-cli-macos-arm64.pkg
   ```

1. From the output, locate the **SHA256 fingerprint** for **Developer ID Installer: AMZN Mobile LLC**\. The following is an example:

   ```
   Package "aws-sam-cli-macos-arm64.pkg":
      Status: signed by a developer certificate issued by Apple for distribution
      Notarization: trusted by the Apple notary service
      Signed with a trusted timestamp on: 2023-05-16 20:29:29 +0000
      Certificate Chain:
       1. Developer ID Installer: AMZN Mobile LLC (94KV3E626L)
          Expires: 2027-06-28 22:57:06 +0000
          SHA256 Fingerprint:
              49 68 39 4A BA 83 3B F0 CC 5E 98 3B E7 C1 72 AC 85 97 65 18 B9 4C
              BA 34 62 BF E9 23 76 98 C5 DA
          ------------------------------------------------------------------------
       2. Developer ID Certification Authority
          Expires: 2031-09-17 00:00:00 +0000
          SHA256 Fingerprint:
              F1 6C D3 C5 4C 7F 83 CE A4 BF 1A 3E 6A 08 19 C8 AA A8 E4 A1 52 8F
              D1 44 71 5F 35 06 43 D2 DF 3A
          ------------------------------------------------------------------------
       3. Apple Root CA
          Expires: 2035-02-09 21:40:36 +0000
          SHA256 Fingerprint:
              B0 B1 73 0E CB C7 FF 45 05 14 2C 49 F1 29 5E 6E DA 6B CA ED 7E 2C
              68 C5 BE 91 B5 A1 10 01 F0 24
   ```

1. The **Developer ID Installer: AMZN Mobile LLC SHA256 fingerprint** should match the following value:

   ```
   49 68 39 4A BA 83 3B F0 CC 5E 98 3B E7 C1 72 AC 85 97 65 18 B9 4C BA 34 62 BF E9 23 76 98 C5 DA
   ```

   If the fingerprint string doesn’t match, do not use the AWS SAM CLI installer\. Escalate to the AWS SAM team by [creating an issue](https://github.com/aws/aws-sam-cli/issues/new?assignees=&labels=stage%2Fneeds-triage&projects=&template=Bug_report.md&title=Bug%3A+TITLE) in the *aws\-sam\-cli GitHub repository*\. If the fingerprint string does match, you can move forward with using the package installer\.

**To verify the package installer manually**
+ See [How to verify the authenticity of manually downloaded Apple software updates](https://support.apple.com/en-us/HT202369) at the *Apple support website*\.

### Windows<a name="reference-sam-cli-install-verify-signature-windows"></a>

The AWS SAM CLI installer is packaged as MSI files for the Windows operating system\.

**To verify the integrity of the installer**

1. Right\-click on the installer and open the **Properties** window\.

1. Choose the **Digital Signatures** tab\.

1. From the **Signature List**, choose **Amazon Web Services, Inc\.**, and then choose **Details**\.

1. Choose the **General** tab, if not already selected, and then choose **View Certificate**\.

1. Choose the **Details** tab, and then choose **All** in the **Show** dropdown list, if not already selected\.

1. Scroll down until you see the **Thumbprint** field and then choose **Thumbprint**\. This displays the entire thumbprint value in the lower window\.

1. Match the thumbprint value to the following value\. If the value matches, move forward with installation\. If not, escalate to the AWS SAM team by [creating an issue](https://github.com/aws/aws-sam-cli/issues/new?assignees=&labels=stage%2Fneeds-triage&projects=&template=Bug_report.md&title=Bug%3A+TITLE) in the *aws\-sam\-cli GitHub repository*\.

   ```
   F2 8D EB E5 8B 21 78 C9 34 27 CD 3D 0F 8B 24 CE 12 8F A0 D1
   ```

## Verify the hash value<a name="reference-sam-cli-install-verify-hash"></a>

### Linux<a name="reference-sam-cli-install-verify-hash-linux"></a>

#### x86\_64 \- command line installer<a name="reference-sam-cli-install-verify-hash-linux-x8664"></a>

Verify the integrity and authenticity of the downloaded installer files by generating a hash value using the following command:

```
$ sha256sum aws-sam-cli-linux-x86_64.zip
```

The output should look like the following example:

```
<64-character SHA256 hash value> aws-sam-cli-linux-x86_64.zip
```

Compare the 64\-character SHA\-256 hash value with the one for your desired AWS SAM CLI version in the [AWS SAM CLI release notes](https://github.com/aws/aws-sam-cli/releases/latest) on GitHub\.

### macOS<a name="reference-sam-cli-install-verify-hash-macos"></a>

#### GUI and command line installer<a name="reference-sam-cli-install-verify-hash-macos-installer"></a>

 Verify the integrity and authenticity of the downloaded installer by generating a hash value using the following command: 

```
$ shasum -a 256 path-to-pkg-installer/name-of-pkg-installer

# Examples
$ shasum -a 256 /Users/myUser/Downloads/aws-sam-cli-macos-arm64.pkg
$ shasum -a 256 /Users/myUser/Downloads/aws-sam-cli-macos-x86_64.pkg
```

 Compare your 64\-character SHA\-256 hash value with the corresponding value in the [AWS SAM CLI release notes](https://github.com/aws/aws-sam-cli/releases/latest) GitHub repository\. 