**This work is based on https://github.com/rgl/mail-vagrant**


This is a [Vagrant](https://www.vagrantup.com/) Environment for a Mail Server. It provides the [Message Transfer Agent (MTA)](https://en.wikipedia.org/wiki/Message_transfer_agent) and the [Mail Delivery Agent (MDA)](https://en.wikipedia.org/wiki/Mail_delivery_agent).

This lets you easily test your application code against a real sandboxed Mail Server.

It uses the following software stack:

* [Postfix](http://www.postfix.org/) to the handle mail storage, reception, and transmission using the [Simple Mail Transfer Protocol (SMTP)](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol).
  * Also show how to configure Postfix in Satellite mode to relay emails to the Postfix server.
  * Also show how to configure nullmailer to relay emails to the Postfix server.
* [Dovecot](http://www.dovecot.org/) to access the mail storage using the [Internet Message Access Protocol (IMAP)](https://en.wikipedia.org/wiki/Internet_Message_Access_Protocol).
* Dovecot for providing User Authentication to Postfix ([SMTP AUTH](https://en.wikipedia.org/wiki/SMTP_Authentication)) through the [Simple Authentication and Security Layer (SASL)](https://en.wikipedia.org/wiki/Simple_Authentication_and_Security_Layer).
* [Dnsmasq](http://thekelleys.org.uk/dnsmasq/doc.html) to handle the internal [Domain Name System (DNS)](https://en.wikipedia.org/wiki/Domain_Name_System).
* [nginx](http://nginx.org/en/) to serve the [Automatic Mail Account Configuration (aka Autoconfiguration)](https://wiki.mozilla.org/Thunderbird:Autoconfiguration:ConfigFileFormat) endpoint.

# Usage

Build and install the [Ubuntu Base Box](https://github.com/rgl/ubuntu-vagrant).

Run `vagrant up mail` to configure the `mail.example.com` mail server environment.

Run `vagrant up satellite` to configure the `satellite.example.com` environment in Postfix Satellite mode that relays all mails to the mail server environment.

Configure your system `/etc/hosts` file with the `example.com` and `mail.example.com` domains:

    192.168.33.254 example.com
    192.168.33.254 mail.example.com

Access http://mail.example.com and follow the instructions to configure your Mail Client with a pre-configured account (all use the `password` password):

    alice@example.com
    bob@example.com
    carol@example.com
    dave@example.com
    eve@example.com
    frank@example.com
    grace@example.com
    henry@example.com

This also has some pre-configured aliases to `alice@example.com`:

    root
    abuse
    postmaster
    hostmaster
    mailer-daemon

At http://mail.example.com/examples you have some examples on how to programmatically use the mail server (e.g. from Python).

To troubleshoot, watch the Mail Server logs with `vagrant ssh` and `journalctl --follow`.
