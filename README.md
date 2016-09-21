# Transform your AWS VPN Generic Config to a Mikrotik set-up script

## Problem description
Unfortunately AWS doesn't support MikroTik in predefined configuration to VPC connect.

We were struggling for a few days now to set up a VPN connection into AWS, because of a MikroTik limitation (http://rant.gulbrandsen.priv.no/mikrotik/ipsec-policy-bugs) and the lack of general documentation as well.

We have created a script that will transform your Generic (Vendor Agnostic) AWS VPN Configuration guide, that you can download from the AWS console into a MikroTik specific configuration script that you can copy-paste into your MikroTik SSH console.

Obviously, we are not accountable for any trouble that this causes to you or your organization, so use it on your own risk.

Thanks Mate Lang for the original script.

## Usage example
```
# You have to give the script one argument,
# the path of the file you downloaded from AWS
# Example:
[mate@devmate]$ ./static-router-config ~/Downloads/vpn-12345abc.txt

Type in local network CIDR (Enter to use guessed 192.168.1.0/24):
Type in your VPC CIDR [10.0.0.0/16]):

Your configuration will be created by using the following values
Your public adddress: 1.2.3.4
Your local network CIDR: 192.168.1.0/24
Your VPC's CIDR: 10.0.0.0/16

AWS Tunnel #1 - Public Address: 5.6.7.8
AWS Tunnel #1 - Inside Customer Gateway Address: 169.254.x.x
AWS Tunnel #1 - Inside Virtual Gateway Address: 169.254.x.x
AWS Tunnel #1 - Secret: THISISVEEEERYVEEERYSECRET

AWS Tunnel #2 - Public Address: 10.11.12.13
AWS Tunnel #2 - Inside Customer Gateway Address: 169.254.y.y
AWS Tunnel #2 - Inside Virtual Gateway Address: 169.254.y.y
AWS Tunnel #2 - Secret: THISISVEEEERYVEEERYSECRET

Is this correct(y/n)? y
Generate the config file in [./mikrotik-aws-config]:
Your config file has been generated in mikrotik-aws-config
```

Now just copy paste the contents of the generated config file into MikroTik's SSH console and you should be up and running.

> Note:
>
> Do not forget to add static routes from AWS back to your home network as well.
>
> Also, make sure you have your route tables correctly set up,
> and define routes back to your home network.

##Dynamic routing config
It's possible to use the dynamic configuration too. The script will ask some other parameters.

```
[fams@nomade]:Amazon $ ./dynamic-router-config vpn-123456.txt
Type in local network CIDR (Enter to use guessed 192.168.0.0/24):
Type in local MKT interface (Enter to use guessed ether1-local): ether1-lan
Type in PUBLIC MKT interface (Enter to use guessed ether2-internet): ether2-inter
Type in your VPC CIDR [10.0.0.0/16]): 10.0.0.0/16

Your configuration will be created by using the following values
Your public adddress: 1.2.3.4
Your local network CIDR: 192.168.0.0/24
Your VPC's CIDR: 10.0.0.0/16

AWS Tunnel #1 - Public Address: 5.6.7.8
AWS Tunnel #1 - Inside Customer Gateway Address: 169.254.X.X
AWS Tunnel #1 - Inside Virtual Gateway Address: 169.254.X.X
AWS Tunnel #1 - Secret: THISISVEEEERYVEEERYSECRET
AWS Tunnel #1 - Customer ASN: 65000
AWS Tunnel #1 - Virtual Gateway ASN: 7224

AWS Tunnel #2 - Public Address: 10.11.12.13
AWS Tunnel #2 - Inside Customer Gateway Address: 169.254.y.y
AWS Tunnel #2 - Inside Virtual Gateway Address: 169.254.y.y
AWS Tunnel #2 - Secret: THISISVEEEERYVEEERYSECRET
AWS Tunnel #2 - Customer ASN: 65000
AWS Tunnel #2 - Virtual Gateway ASN: 7224

Is this correct(y/n)? y
Generate the config file in [./mikrotik-aws-config]:
Your config file has been generated in mikrotik-aws-config
```
# Kudos
Kudos go out to these guys who wrote blog posts on this topic and shared my pain.
* http://biplane.com.au/blog/?p=406
* http://rant.gulbrandsen.priv.no/amazon/mikrotik-aws-ipsec
* http://forum.mikrotik.com/viewtopic.php?t=87844

# Contributions
Feel free to fork and improve or contribute.

May the source be with you.
