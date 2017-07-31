---
title: 'The Basics of hledger'
date: '2017-07-30'
categories: ['introduction']
tags: ['ledger','formatting','installation','Haskell Stack','Simon Michael','John Wiegley','add', 'nano', 'gedit', 'print']
---

So what exactly is **hledger**? Basically, it's a program that parses a plain-text *journal* file and uses it to generate financial reports. The journal itself is formatted for double-entry accounting, i.e. every credit must have a corresponding debit. The core **hledger** program operates exclusively from a terminal command line, although there are other interfaces available.

## Creating the Journal & Basic Commands

You can use any text editor to create or modify the journal. (I use **nano** or **gedit** personally.) There is also a built-in command called ``hledger add`` that lets you create a new journal or add entries to an existing file. This command, however, cannot be used to edit or modify journal entries; that can only be done with a text editor. 

By default, **hledger** looks for the journal in your home directory at ``~/.hledger.journal``. But you can use any file as the journal by adding the ``-f`` flag. Say you have a journal file located at ``~/Documents/sample.journal``. To have **hledger** print out all of the entries in this journal you would enter:

        $ hledger print -f ~/Documents/sample.journal 

You'll note that ``hledger`` must be followed by a command. If you enter ``hledger`` alone, you will get a help message with a list of available commands. In addition to ``add`` and ``print``, some of the other basic **hledger** commands include:

        $ hledger accounts      # prints a list of accounts
        $ hledger balancesheet  # prints a list of accounts and balances
        $ hledger register      # prints a list of transactions and running balances

Most of these commands also have abbreviations, such as ``hledger bal`` for ``hledger balance`` and ``hledger bs`` for ``hledger balancesheet``. 

In working with the journal itself, there are a few basic formatting rules that must be followed:

1. Each entry begins with a non-indented date starting with the four-digit year (i.e., 2017/07/30);
2. After the date, and staying on the same line, is a space followed by a description of the journal entry;
3. There are at least two additional lines that are indented, each containing an account name and a transaction amount; and
4.  There must be **at least two spaces** between the account name and transaction amount.

This last rule is critical. Here is an example of a correctly formatted journal entry:

        2017/07/30 Sample entry
            assets   100
            equity  -100

Here is an incorrect example:

        2017/07/30 Incorrect entry
            assets 100
            equity -100

With the second example, **hledger** will read the entry as an account called ``assets 100`` rather than an ``assets`` account with a $100 debit. 

## How Do I Install hledger?

**Hledger** is written in the Haskell programming language. The best way I've found to install the program is through [**Haskell Stack**](https://haskell-lang.org/get-started), which is the official builder for multi-package Haskell projects. You can learn more about Stack and other installation options through the [**hledger** download page](http://hledger.org/download.html).

Some Linux distributions also maintain a pre-compiled **hledger** package. These packages are often several versions behind the current release. [**Debian**](https://www.debian.org/), for instance, currently has [**hledger 1.0.1**](https://tracker.debian.org/pkg/haskell-hledger) in its *stable* repository, while the most recent upstream release, as of this writing, is **hledger 1.3**. 

For purposes of this blog, I try to stay on the most current release. I have **hledger 1.3** installed (via Haskell Stack) on a ThinkPad T420 running [**Solus**](https://solus-project.com), an independent Linux-based operating system. 

## Hledger vs. Ledger

[Simon Michael](https://github.com/simonmichael) originally developed **hledger** as a Haskell-based reimplementation of **Ledger**, a plain-text accounting tool first released by John Wiegley in 2003. The [**hledger** documentation](http://hledger.org/faq.html#hledger-and-ledger) offers a detailed explanation of the differences between the two programs.

While this blog will focus on **hledger**, its journal files should also work in **Ledger**. (**Ledger** does not have an ``add`` command, however, so you need to create journals exclusively with a text editor.) Since **Ledger** is more widely available through Linux and BSD package managers, you may want to use it if for some reason you are unable to install **hledger**. 
