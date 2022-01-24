+++
title = "Ditching Google's Mail"
author = ["Roberto Zoia"]
date = 2022-01-24
tags = ["100Words"]
slug = "ditching-google-mail"
draft = false
+++
Today I finally ditched Google for my personal domain's email.

Google has announced that on May 1, 2022, it's ending the free tier I've been using for more than 10 years to host my domain's email. I knew this was coming long ago, but I was lazy.

The easiest way to solve this is moving the kids email accounts to free email accounts, and paying Google $3/user monthly for the remaining accounts for the first year and $6/user afterwards[^google-pricing]. I don't like this solution. For many reasons, I'm not so fond of Google the _advertising company_ anymore. Why would I choose for my kids a free email provider with most of the issues I'm trying to avoid by moving away from Google?

[^google-pricing]: Google is, by the way, one of the lowest-priced mail services, per user, that you'll find.

My main criteria for looking for a new provider, aside from pricing considerations, was looking for a stable company with supports for open standards, i.e., IMAP and SMTP. This is important because I want to minimize vendor lock-in. For example, it allows me to keep a local backup my email.

For example, [Hey](https://hey.com) may be a great platform from the email-workflow point of view. I have great respect for Basecamp and its founders. But not being able to import my existing messages to their platform is a deal breaker for me. Something similar applies to ProtonMail and other alternatives.

## Apple Blues

My first attempt was trying iCloud+ custom domain's feature. Maybe you don't like Apple. Apple as a company may have its flaws, but selling your information to third parties or intentionally compromising your security and privacy is not one of them.

iCloud+ custom domains would have allowed me to create an email account for each family member, using the storage I'm already paying for. It didn't work, however. Innocent of me. I should have suspected of anyone recommending to surround your SPF record with double double-quotes. I spent _hours_ tweaking my DNS configuration, even changed DNS servers... but iCloud+ refused my domain insisting it couldn't find my SPF records. ([mxtoolbox](https://mxtoolbox.com/) had no trouble finding the records, however.)

I searched for a solution in countless forums, subreddits, etc. I commiserated with other people with SPF records problems. Finally, I found what seems the most likely explanation: iCloud+ doesn't allow you to use a domain associated with your Apple ID as a custom domain. Anyway, by then iCloud+ custom domains had more than exhausted my time and patience without any results. Bad starter for what should be a long term relationship.

## Migadu

After discarding naive and dangerous thoughts about self-hosting my email, I remembered about Migadu. I found about [Migadu](https://migadu.com) thanks to [Drew DeVault's excellent blog](https://drewdevault.com/2020/06/19/Mail-service-provider-recommendations.html). They not only offer fair pricing and email support, but they base their pricing on resource allocation, not user accounts. That means you pay for storage and bandwidth, and can create as many email accounts for your domain as you need.

I signed for a trial account and set up my DNS records as recommended by Migadu's no-nonsense clear documentation. In _minutes_ I was using `imapsync` to copy my mail from Google's servers to Migadu. It worked flawlessly, the first time. (Copying everything took longer because of the volume of messages involved.)

In 30 minutes I was changing my trial to a paid plan.
