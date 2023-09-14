---
layout: post
title:  SNI-Changer using Mitm-Proxy
tags: [linux, c, OpenSSL]
image: /assets/posts/sni-changer-using-mitm-proxy/sni-changer.png
---

## Overview

The SNI-Changer is a tool designed to change the SNI extension of the ClientHello message. To do this, a TLS connection is established with the user, pretending to be the server, thus providing a certificate signed by a user-created root certificate. With the target server, another TLS connection is established, modifying one of the extensions of the TLS protocol, the Server Name Indication (SNI). After both of these connections are in place, any data transmitted between the user and the server is redirected to the opposite party.

![image](/assets/posts/sni-changer-using-mitm-proxy/sni-changer-using-mitm-proxy.png)

## What is the ClientHello message?
When a client (such as a web browser) initiates a secure connection with a server using HTTPS (HTTP Secure), it begins with a step called the "Client Hello". This initial message serves as a greeting and a request to establish a secure connection using the Transport Layer Security (TLS) protocol.

## What is SNI?
The Server Name Indication (SNI) is a part of the Client Hello message. It's especially important in scenarios where a single server hosts multiple websites or services, each with its own domain name and SSL/TLS certificate. Before SNI, servers could only present a single certificate, often for the default website hosted on the server. SNI resolves this challenge by enabling the client to specify the domain name it's trying to access during the Client Hello.

## Why change the SNI?
According to the paper [Efficiently Bypassing SNI-based HTTPS Filtering](https://dl.ifip.org/db/conf/im/im2015exp/137348.pdf), there are two different ways to change the SNI to bypass the Firewall:
- Bypassing Based on Backward Compatibility
- Bypassing Based on Shared Server Certificate

## Technologies used

The **C language** was used with the **OpenSSL** library for the establishment of connections and certificate creation.