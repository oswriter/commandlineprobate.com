---
title: 'Introduction to Command Line Probate'
date: '2017-07-05'
categories: ['introduction']
tags: ['probate', 'plain-text accounting', 'ledger']
---

Have you ever served as the executor of someone's estate? Or are you named as the executor in the will of your spouse, parent, or sibling? At some point, most of us will be asked to handle the "final affairs" of a family member or close friend. 

Aside from perhaps jury duty, administering an estate is probably the most common legal role assigned to the layperson. And while a good probate attorney can (and should) assist with opening and closing an estate, it is ultimately the executor's responsibility. The executor--also known as the "personal representative" or "administrator" depending on the state and circumstances of the appointment--is the person charged with gathering the assets of the deceased, paying any valid debts and administration expenses, and distributing the remainder to the appropriate heirs or beneficiaries.

This process is called *probate*. While the exact requirements of probate vary from state to state, a common denominator is the need for accurate accounting. In some cases, an executor must submit a formal probate accounting to a judge before the estate can be formally closed. But even in less formal probate proceedings, it is important to keep accurate records of all assets that come into--and go out of--the estate.

## Why Estates Require Double-Entry Accounting

How many of you actually balance your checking account each month? In the age of online banking, where we can instantly access our balances using a smartphone app, many people do not bother with any sort of formal bookkeeping system. Unfortunately, such a laissez-faire approach is not acceptable when managing a probate estate.

Double-entry accounting is a critical tool in probate estate administration. Basically, every transaction affecting the estate's finances is recorded twice--once as a *debit*, and once as a *credit*. The sum of all debits and credits should equal each other, or *balance*. In business accounting, this balancing principle is expressed with the following equation:

        Assets = Liabilities + Equity

In probate accounting, this equation can be modified to be read as:

        Receipts = Disbursements + Distributions

The left side of the equation represents the money (or other property) that comes into the estate, while the right side shows those same assets going back out. In a business firm, *equity* represents the assets retained by the owners of the company. This concept does not apply to a probate estate. An estate must eventually close, leaving an "equity" of zero. The beneficiaries of the estate are essentially the "shareholders" in that they are the residual claimants of any remaining assets.

## Can't I Just Have the Attorney Do the Books?

In my professional career, I spent over 15 years as a trust and estate paralegal. One of my jobs was to handle the accounting for probate estates. Many times an executor would just hand over a half-completed checkbook register and a pile of unorganized receipts. I would then spend hours--and often days--organizing the data into a presentable account.

From the estate's perspective, this was a waste of money. An experienced estate attorney can charge $300-$400 per hour for their time plus another $100-$200 for their paralegal. In other words, if it takes the paralegal five hours to sort out the accounts--and another hour for the attorney to review that work--the estate could be billed $1,400 for simple bookkeeping tasks. 

There's also the potential waste of time. As a paralegal, if I had incomplete or inaccurate financial data, I had to inform the attorney, who in turn had to contact the executor. It might take several days or weeks to get the information I needed, thereby delaying completion of the estate account. In the end, an executor who keeps complete, accurate financial records helps themselves, the attorney, and the estate's beneficiaries. 

## Hledger and Plain-text Accounting

This leads to the obvious question: How do you keep track of estate accounts using a double-entry system? You could use spreadsheets. I've done this and it's not ideal. Since everything has to balance, a simple data-entry error can throw the entire spreadsheet off, and it can take hours to identify and correct the problem.

Obviously, there are a number of highly sophisticated software applications like QuickBooks and Quicken. But if you're not already familiar with these programs, there can be a steep learning curve. Additionally, most accounting software uses predefined categories for business or personal use, rather than probate estates.

A few years ago, when I was looking for a simple, easy-to-configure tool to help me with probate accounting, I discovered [**hledger**](http://hledger.org/). Hledger belongs to a category of software known as [*plain-text accounting*](http://plaintextaccounting.org/). Hledger was "inspired" by [**ledger**](http://ledger-cli.org/), a "double-entry accounting system that is accessed from the UNIX command-line." 

Like ledger, hledger relies on simple text "journals" to provide all of the necessary financial data. The user then runs hledger from inside a terminal with a qualifying command. For example, if I wanted hledger to display all of the current account balances I would enter ``hledger balance``. Hledger itself does not modify the journal. It simply parses the existing data in the text file.

## What This Blog Will (and Will Not) Do

I wanted to document my experiences using hledger as a tool for probate accounting. In addition, I plan to more fully explore all of the potential of hledger and its related tools. Hledger is one of the most outstanding examples of an open-source software project, one that is not only free to download and use, but also to modify and help develop. Since I'm not a programmer, I figured the best way to contribute was to provide some practical, "real-world" documentation.

At this point, I must reiterate that while I have experience as a paralegal, I am not a licensed attorney. Nothing presented on this blog should be construed as legal advice. This is a guide to using software. If you are the executor of an estate now or in the future, I hope you find this information useful in helping to prepare financial records for your probate attorney or accountant. You should **always** seek qualified help from a licensed professional when managing a probate estate.

With those caveats, I look forward to working on this blog. If you are a Linux professional, I hope you find these tutorials helpful. In keeping with open-source standards, this blog's content is licensed under a [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) license. All of the source files for the blog are also available on [Github](https://github.com/oswriter/commandlineprobate.com).  
