---
title: 'Inventory, Part I: Will It Probate?'
date: '2017-08-31'
categories: ['inventory']

---

The *inventory* lists all of the assets in the probate estate. But what exactly do we mean by *probate estate*? In many cases, a person may have substantial assets but little or no probate estate. This is because the probate estate only refers to assets that are owned and titled in a particular way.

Perhaps the best way to explain this is by reference to user and group permissions in Linux. Think of a directory containing several files. Each file belongs to an *user* and a *group*. The group allows multiple users to access, and possibly modify, the file.

Along similar lines, a person may have ownership interests in several assets, each of which belongs to a particular "group." One of these is the "probate" group. But there are also multiple non-probate groups. Each group has a particular method for titling and disposing of an asset after the "user" dies.

## Dividing Assets Into Groups

Let's consider a hypothetical "user" (jsmith) who has the following asset "files":

User    | Group  | File
--------|--------|-----
jsmith  | trust  | house
jsmith  | trust  | rental-property
jsmith  | probate| car
jsmith  | tod    | brokerage-account
jsmith  | tod    | IRA
jsmith  | jtwrs  | checking-account
jsmith  | probate| savings-account
jsmith  | probate| savings-bonds

Based on this, jsmith's probate estate would only consist of three assets: a car, a savings account, and some savings bonds. These are the only assets that would be reported on the inventory and dealt with in the subsequent probate account. All other assets would pass outside of probate.

So what do all of the non-probate groups mean? Here's a brief rundown:

### Trusts

A common tool for bypassing probate is the creation of a *trust*. In a trust you have three variables:

1. Settlor
2. Trustee
3. Beneficiary

In a typical estate planning trust--usually called a *revocable living trust*--all three of these variables refer to the same person. In other words, Jane Smith (as settlor) gives assets to Jane Smith (as trustee) for the benefit of Jane Smith during her lifetime.

Much like a program, the trust also provides instructions for what happens when these variables changes. In other words, when the settlor dies, the trust designates a successor trustee, one or more contingent beneficiaries, and directions on when and how to distribute any remaining trust assets to those beneficiaries.

Since assets in a trust are titled in the name of the trustee, they are not considered probate assets of the settlor--even though the settlor retains the right to revoke the trust at any time. The trust instrument should include one or more schedules listing the assets transferred into the trust. And for real property, the deed should state that the trustee is the lawful owner.

There are also trusts created as part of a person's last will and testament. These are known as *testementary trusts*. I'll address those in a future post, as they often affect the final distribution of a probate estate.  

### Transfer on Death Assets

In my hypothetical list above, I included jsmith's brokerage account and individual retirement account (IRA) in a group identified as "TOD." This is shorthand for *transfer on death*, which is also known as *payable on death* (POD). These are assets that remain the property of the individual owner--they are not part of a trust--but title automatically passes to a designated beneficiary upon death.

IRAs, 401(k) plans, and similar retirement accounts are almost always TOD assets. This is due to the fact that federal law governs such accounts. A beneficiary designation for a retirement account overrules a contrary designation in the account holder's will. Many people also use POD bank or brokerage accounts to ensure a spouse, child, or other relative has immediate access to capital after their death.

### Joint Tenancy With Right of Survivorship

The checking account listed above is in the group "JTWRS," which stands for *joint tenant with right of survivorship*. This refers to the existence of a co-owner who has the automatic right to sole ownership of the asset once the other "tenant" dies. As with a TOD/POD asset, the property held in joint tenancy does not pass as part of the deceased co-owner's probate estate.

## Creating an Account Tree

Once you sort out which assets belong to the probate "group," you can start to prepare an inventory. Since **hledger** does not come with a pre-configured chart of accounts, you need to plan and implement your own *account tree*. Ideally, your account tree should track the inventory categories used by the probate court's model inventory or accounting forms.

This is a good point to pause and note that for most of the examples going forward on this blog, I will be using probate forms and rules from the [State of Maryland](http://registers.maryland.gov), since that is the jurisdiction where I have the most firsthand experience. And while probate laws are more alike than different throughout the United States, each state has its own specific way of doing things. That is why you should never administer any probate estate without the assistance of an attorney knowledgeable in the applicable state's laws.

Anyhow, Maryland's [standard inventory form](http://registers.maryland.gov/main/forms/RW1122and1123.pdf) includes seven categories of assets:

1. Real property
2. Leasehold property
3. Tangible personal property
4. Corporate stocks
5. Bonds, notes, mortgages, debts due to the decedent
6. Bank accounts, savings and loan accounts, cash
7. All other assets

Most estates will not use every category. But it provides a useful starting point for planning a "tree" of accounts.

Remember, **hledger** defines accounts and sub-accounts using colon-separated entries. In the [simple first account](http://localhost:1313/post/002-a-simple-first-account/) described in my last post, for example, I classified a checking account with the entry ``assets:aunt's checking account``. You should always begin any asset-related account with ``assets``, since **hledger** will look for this in preparing certain reports. After that, it is pretty much up to you how to classify any sub-accounts.

My approach is to use the state inventory form's categories as the first-level sub-account, followed by a second-level sub-account for each individual probate asset. For instance, let's assume all of the "jsmith" assets in the table above are probate assets. Here is how I would build the account tree:

    assets
      real property
        house
        rental property
      tangible personal property
        car
      corporate stocks
        brokerage account
      bonds
        savings bonds
      bank accounts
        checking account
        savings account
      other interests
        IRA

Now, **hledger** builds the account tree from individual transactions, so you need to be careful when entering data. For example, if you enter this:

    2017/03/15 checking account
        assets:bank accounts:checking account    20000
        inventory                               -20000.0

    2017/03/15 savings account
        assets:savings account                  15000
        inventory                              -15000.0

Here is how **hledger** will build the account tree:

    $ hledger accounts --tree
      assets
        bank accounts
          checking account
        savings account
      inventory

So if you want the savings account under ``bank accounts,`` it needs to be entered as ``assets:bank accounts:savings account``. Also note you can insert single spaces between the words of account names. But if you enter a double space, **hledger** will return an error message, since it is expecting a dollar amount rather than more text.

## What's Next?

Now that you have an overall view of the types of assets that are included in a probate estate, as well as how to plan an account tree, I'll move into describing how to classify and value specific types of assets in building the inventory. In the next post, I'll start with the largest asset in many probate estates--real estate.
