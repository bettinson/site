---
layout: post
title: Backend is fun!
---

At Shopify, I was recently responsible for refactoring an internal model to display alerts on an orders page to the merchant.
So, if a merchant did not have Paypal set up and they needed to, an alert would be generated and displayed. Before, this was a bit of a mess of structs in one gigantic class; it was a textbook example of not being able to predict the future and letting one class have too much responsibility. This was my first refactor ever. What I didn't realize was how fun a refactor would be until someone else created an alert class following the patterns I'd written! The feeling of making a part of the codebase better than I'd left it and people using my work as an example to extend existing functionality was wonderful. Now that I'm writing more front-end focused code, I'm realizing how much I enjoy being behind the scenes. 

However, right now, I'm working on fixing an interesting sorting bug in our internal pagination code, so I get to write back-end code while I implement frontend fixes.