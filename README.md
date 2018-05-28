# swit_signers_openpgp_signer
## OpenPGP Signer for TYPO3

Just bind into your TYPO3 extension and change VENDOR and MyExtension to your namespace.

You need to compile php with gnupg support enabled.

Allowed (public) keys have to  be assigned to the gnupg keyring of your current webuser.

Your sending email address must have a valid key pair on this server.

```php
        /** @var MailMessage $message */
        $message = $this->objectManager->get('TYPO3\\CMS\\Core\\Mail\\MailMessage');
        $message->setTo($recipient)->setFrom($sender)->setSubject($subject);
        $signer = new \VENDOR\MyExtension\Helper\SwiftSignersOpenPGPSigner();
        foreach ($recipient as $email => $item) {
            $signer->addRecipient($item);
        }
        $message->attachSigner($signer);
        $message->setBody($emailBody, 'text/html');
        $message->send();
```
Inspired by: https://github.com/Mailgarant/switfmailer-openpgp
