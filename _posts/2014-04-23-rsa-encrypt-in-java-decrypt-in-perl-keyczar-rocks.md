---
layout: post
title: "RSA Encrypt in Java Decrypt in Perl: keyczar rocks"
description: "RSA Encrypt in Java Decrypt in Perl"
category: "Perl"
tags: ["Perl", "Java", "RSA", "Encrpyt", "Decrypt"]
---
{% include JB/setup %}

I have been struggling with Java RSA decrypt for a long time last night until I meet [keyczar](http://www.keyczar.org/)

the case is that we developed an API login which is used in a mobile App. but it's quite insecure to pass the plain password directly to server. so it must be encrpyted in Java (Android App) then post to the Perl API.

the Java is using something like below to encrypt the pass
```
Cipher cipher = Cipher.getInstance("RSA/ECB/PKCS1Padding");
cipher.init(Cipher.ENCRYPT_MODE, key);
return cipher.doFinal(data);
```

then decrypt with
```
Cipher cipher = Cipher.getInstance("RSA/ECB/PKCS1Padding");
cipher.init(Cipher.DECRYPT_MODE, key);
return cipher.doFinal(cipherData);
```

it was a nightware to find equivalent code in Perl. RSA+EBC+PKCS1Padding, no luck with a lots of RSA modules tried.

until I found the [Crypt::Keyczar](https://metacpan.org/pod/Crypt::Keyczar). it saves a lot. the author wrote a very good file to do the [Java magic](https://github.com/oyama/Crypt-Keyczar/blob/master/t/compat-java/Makefile). with the make running, you got a crypt-rsa and crypt-rsa-pub created. actually it's done by [KeyczarTool](https://code.google.com/p/keyczar/wiki/KeyczarTool)

```
create --location=crypt-rsa --purpose=crypt --asymmetric=rsa
addkey --location=crypt-rsa --status=primary
pubkey --location=crypt-rsa --destination=crypt-rsa-pub
```

after that, we encrypt the string in Java with code like:
```
import org.keyczar.*;

public class demo {
    public static void main(String[] args) throws Exception {
        KeyczarFileReader reader = new KeyczarFileReader("./crypt-rsa-pub");
        try {
            Encrypter crypter = new Encrypter(reader);
            System.out.print(crypter.encrypt("hello") + "\n");

        } catch (org.keyczar.exceptions.KeyczarException e) {
            System.out.print("ng\n");
        }
    }
}
```

sample output:
```
$ export CLASSPATH="log4j.jar:gson.jar:keyczar.jar:."
$ javac demo.java
$ java demo
AG1jZrM2CFMhPpNegCx5jletymyJ_9-DlkIgigYo83WCiF6tkTRpotg754LRIjy8ILMSA6Q4AMTg0YD7EgiI6S2rLE1r9lwOYIc0E84tKSWJ3tw0QEBeCLPwuotZbHB92K2Dkuylp3dsP3ESG7rD_RLQylITssyUgNmzdDOGNfmLRJE9XSvJMw3jov3unvLp0iBsK5E71ntsU56kRRXGAI37-tRxo3mmcQZkkozdrS_2p0QZ4zQ08rjCYbCMlrl_xdMlOB3fd1y-HujLHzYID0lb83gW_o5pX2gurldU0-nB2bitgH21pQuPRQz1qEy5zW1TLkOkDX66uqIowHA08R-ueWKSwkm72MbdWvdUmuA-NtkY7IJ-1wRW6HWRaSqbIo3Hz3uPp3j2FfXlNsxtnfdFgV5Hhh348oIjzTE7AGhXSfBE9KB8S0lHGFIxXEc3I43ZIt4gNBbn_nNwhLjzn5hmE_OrlGPKNsoALwLMDGzFQfh7IXfGQmKISfobr5YVv-3ZDes3et8zIEQX9X4iEKLPtX4Jw1qNxFRi715kpXjim1fkya9SjNOYAvwul_Ql16Uvzr2xM0ohip4RuEXNkuqqyLxoF8pS0ISexHiBKLbD23rJy-ZjUPxJa6zXHUW4Fx8r2VPW-03xW5QCxekG1-1zqdUVL9jHti19ObZOzsSjSZ4X9w
```

with Perl code like:
```
use Crypt::Keyczar::Crypter;
use FindBin qw/$Bin/;

my $msg = "AG1jZrM2CFMhPpNegCx5jletymyJ_9-DlkIgigYo83WCiF6tkTRpotg754LRIjy8ILMSA6Q4AMTg0YD7EgiI6S2rLE1r9lwOYIc0E84tKSWJ3tw0QEBeCLPwuotZbHB92K2Dkuylp3dsP3ESG7rD_RLQylITssyUgNmzdDOGNfmLRJE9XSvJMw3jov3unvLp0iBsK5E71ntsU56kRRXGAI37-tRxo3mmcQZkkozdrS_2p0QZ4zQ08rjCYbCMlrl_xdMlOB3fd1y-HujLHzYID0lb83gW_o5pX2gurldU0-nB2bitgH21pQuPRQz1qEy5zW1TLkOkDX66uqIowHA08R-ueWKSwkm72MbdWvdUmuA-NtkY7IJ-1wRW6HWRaSqbIo3Hz3uPp3j2FfXlNsxtnfdFgV5Hhh348oIjzTE7AGhXSfBE9KB8S0lHGFIxXEc3I43ZIt4gNBbn_nNwhLjzn5hmE_OrlGPKNsoALwLMDGzFQfh7IXfGQmKISfobr5YVv-3ZDes3et8zIEQX9X4iEKLPtX4Jw1qNxFRi715kpXjim1fkya9SjNOYAvwul_Ql16Uvzr2xM0ohip4RuEXNkuqqyLxoF8pS0ISexHiBKLbD23rJy-ZjUPxJa6zXHUW4Fx8r2VPW-03xW5QCxekG1-1zqdUVL9jHti19ObZOzsSjSZ4X9w";

my $c = Crypt::Keyczar::Crypter->new("$Bin/crypt-rsa");
print $c->decrypt(Crypt::Keyczar::Util::decode($msg)) . "\n"; ## print hello
```

pretty neat. many thanks to the author. have fun.
