+++
title = "Reveal encrypted email address with echo and sed"
date = 2020-12-02
+++

I remember the first time I published an email address on a website with no obfuscation. If you did it too you
can imagine what my mailbox looked like back then. I have been looking for solutions to prevent robots collecting my
email address and among others I like the way Mathilde does it, mostly because I think it's fun.

So last weeks I asked Mathilde how did she build her fun way to hide her email address on her personal
website [contact page](https://mental.af/contact/). She answered she did it manually. I tried  manually too but it's
painfull so I decided to build a tool to generate the command.

It is pure client-side javascript, using simple substitution cryptography. It generates a command with common
unix utilities `echo` and `sed`. You just need to enter your email address and you'll get the command. You can
share the generated command on your website, your visitors will need to paste it into their terminal emulator
and it will reveal the email address.

You can find the tool [here](https://myrdn.github.io/mail-address-encryption/).
