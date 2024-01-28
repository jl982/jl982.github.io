---
layout: post
title:  How to migrate an AWS EC2 instance from IPv4 to IPv6
date:   2024-01-28
tags: software knowmatic
---

With AWS's decision to [charge for public IPv4 addresses](https://aws.amazon.com/blogs/aws/new-aws-public-ipv4-address-charge-public-ip-insights/){:target="_blank"} starting February 1, 2024, many users are looking for ways to avoid the new cost. This article guides you through the process of assigning an IPv6 address to your Amazon EC2 instance and removing the IPv4 address to prevent incurring charges.

## Check IPv6 Support

Before making any changes to your AWS setup, ensure that your internet connection supports IPv6. You can use an [online site](https://test-ipv6.com/){:target="_blank"} to confirm the support.

## Add IPv6 Address

**VPC**

The first step in the migration process is to configure your Virtual Private Cloud (VPC) to support IPv6.

- Navigate to your VPC settings.
- Select Actions and then Edit CIDRs.
- Assign an IPv6 CIDR block, allowing Amazon to select it for you.

![](/assets/images/2024-01-28-ec2-from-ipv4-to-ipv6/1-k8haynfcpdc2yruh97ucq3zv.gif)

**Subnet**

After setting up your VPC, you need to configure the subnet associated with your EC2 instance.

- Find and click on the relevant subnet.
- Edit the IPv6 CIDR block, assigning a /64 address.

![](/assets/images/2024-01-28-ec2-from-ipv4-to-ipv6/2-y8m2mexsh6qx2y9dh80gcb8g.gif)

**Network Interface**

Next, adjust the network interface settings of your EC2 instance to enable IPv6.

- Go to the instance's network interface.
- Enable IPv6 assignment and set the primary IPv6 IP to be assigned.

![](/assets/images/2024-01-28-ec2-from-ipv4-to-ipv6/3-g61jhz2ycyep8skh1yw28t2i.gif)

**Security Group**

To allow traffic to your instance over IPv6, update the security group settings.

- Add a rule to the security group to accept IPv6 addresses.

![](/assets/images/2024-01-28-ec2-from-ipv4-to-ipv6/4-uoy2b6toqux628l81ow4uru1.gif)

**Route Table**

Ensure that there is a route for IPv6 traffic in your VPC's route table.

- Edit the route table and add a route for IPv6.
- Direct the IPv6 traffic to the same internet gateway used for IPv4.

![](/assets/images/2024-01-28-ec2-from-ipv4-to-ipv6/5-l6cjwjcerd5idgm1yoih2xy0.gif)

Now you can SSH into your EC2 instance using IPv6.

## Remove IPv4 Address

Temporarily associate an Elastic IP with your instance to remove the auto-assigned IPv4 address.

**Allocate and Associate an Elastic IP**

- Allocate a new Elastic IP.
- Associate it with the network interface of your running instance.

![](/assets/images/2024-01-28-ec2-from-ipv4-to-ipv6/6-cqe2sf9r3xcb17616q0bdcb0.gif)

**Create and Attach a New Network Interface**

- Create a new network interface in the correct subnet and assign it the same security group.
- Attach the new network interface to your instance.

![](/assets/images/2024-01-28-ec2-from-ipv4-to-ipv6/7-shdd6r6yadxa5pypeivy2w9r.gif)

**Disassociate and Release the Elastic IP**

Complete the process by dissociating and releasing the Elastic IP.

![](/assets/images/2024-01-28-ec2-from-ipv4-to-ipv6/8-jt4fgye9y1fxzzh8ip9mj8g7.gif)

After completing these steps, your instance will only have an IPv6 address and no longer have a public IPv4 address, ensuring you are not charged for IPv4 usage.

## Created by Knowmatic

I created this guide using [Knowmatic](https://www.knowmatic.app/how-to/){:target="_blank"}, a tool I'm building that allows you to write help-center style articles by simply recording narrated screencasts. Here's the [input video](https://youtu.be/-wjUMIQVklE){:target="_blank"} I recorded (with our browser extension) to generate the above content. As you can see, I was anything but polished the recording - I paused excessively, stumbled with my words, and even had to debug for 20 minutes in the middle when I missed a step in my configurations. But the output article had none of my mishaps. The text is concise and comes with GIFs automatically clipped at the appropriate times.

If Knowmatic's utility appeals to you, [drop us a line](mailto:hello@knowmatic.app), and we'd love to add you to our private beta.

## Discussion

Discuss this post on [HN](https://news.ycombinator.com/item?id=39169208).
