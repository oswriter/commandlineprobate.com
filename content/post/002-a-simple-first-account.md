---
title: 'A Simple First Account'
date: '2017-07-31'
categories: ['introduction']
tags: ['inventory','balance','distribution','debts']

---

The life of a *probate estate* can be broken down into three phases:

1. The inventory phase
2. The administration phase
3. The closing phase

To demonstrate, I will create an **hledger** journal for a very simple hypothetical account. This will be a probate estate with just one asset and a handful of disbursements. Although probate is very state-specific in the United States, this is a generic example, so I won't be delving into any particular state's laws at this point.

## Administering Your (Fictional) Aunt's Estate

Let's say your aunt died on March 15, 2017. She had a will leaving her entire estate to her three favorite nieces and nephews, which includes you. Additionally, you are named the personal representative of the estate.

### Inventory Phase

The *inventory* is a list of probate assets valued as of the date of the person's death. In this hypothetical, your aunt didn't own much. She lived in a relative's apartment and did not own a car or any tangible property worth anything. Her only probate asset is a non-interest-bearing checking account with $20,000.

To begin your **hledger** journal, you make an entry debiting $20,000 to an *asset* account--your aunt's checking account--and crediting a corresponding $20,000 to an *equity* account, which you label as ``inventory``:

        2017/03/15 inventory - checking
            assets:aunt's checking account          20,000
            inventory                              -20,000

If you then check your account balances, **hledger** gives you the following report:

        $ hledger balance
             20000.0  assets:aunt's checking account
            -20000.0  inventory
            --------------------
                   0

Notice the account balances zero out. This is critical. In double-entry bookkeeping the accounts must balance at all times. **Hledger** will produce an error message if the entries do not balance. For example, say you accidentally entered a credit of $2,000--rather than $20,000--for the ``inventory`` account:

        $ hledger balance
        hledger: could not balance this transaction (real postings are off by 18000.0)
        2017/03/15 inventory - checking
            assets:aunt's checking account         20000.0
            inventory                              -2000.0

### Administration Phase

There are a number of tasks that may need to be completed during the administration phase, such as receiving any after-death income, taking care of any final expenses the decedent incurred, and paying for the probate administration itself. For purposes of this simple example, we'll say your fictional aunt had no additional income and only a couple of minor expenses.

Probate estates must typically publish a legal notice to inform any potential creditors or heirs that an estate has been opened and provide the statutory deadline to file any claims. Even in the internet age, such notices still need to be published in a newspaper, which incurs a nominal cost:

        2017/04/01 publication of notice to creditors
            disbursements:administration        60
            assets:aunt's checking account     -60

As you can see, this journal entry creates a new account for ``disbursements``, and a sub-account for ``administration``, which stands for expenses related to the administration of the estate--as opposed to, say, administration of property.

But wait. You cannot pay that publication bill directly from your aunt's checking account. Instead, you need to close her personal checking account and open a new account for the probate estate. You note this *change in assets* with the following journal entry:

        2017/04/01 opening of estate checking account
            assets:estate checking              20000
            assets:aunt's checking account     -20000

Now you can pay the publication costs properly:

        2017/04/01 publication of notice to creditors
            disbursements:administration    	    60
            assets:estate checking  	    	   -60

In response to the notice, your aunt's credit card company sends you a bill for an outstanding balance of $157. As personal representative, you allow the claim and pay the bill:

        2017/04/16 credit card bill
            disbursements:debts                 157
            assets:estate checking             -157

If you now ask **hledger** for a balance report, you get the following:

        $ hledger balance
                     19783.0  assets:estate checking
                       217.0  disbursements
                        60.0    administration
                       157.0    debts
                    -20000.0  inventory
        --------------------
                           0

Note there is no longer an entry for the now-closed ``assets:aunt's checking account`` sub-account. By default, **hledger** does not display any accounts with a zero balance.

To keep this example simple, we'll assume there are no further administration expenses or debts. The only final expense will be for court costs. In most states, there is a *probate fee* assessed to defray the costs for administering the estate. For this example we'll assume the probate fee is $150:

        2017/12/15 probate fee
            disbursements:court costs       150
            assets:estate checking         -150

A brief explanation of the date: There is usually a minimum period that an estate must be kept open. This is to ensure creditors and potential heirs have adequate time to respond to the published notice. For purposes of this example we'll assume the waiting period is nine months, meaning the estate cannot be closed until the end of December, since your aunt died in March.

### Closing Phase

Finally, the estate is ready to be closed. For multi-million dollar estates there might be federal or state taxes that need to be paid at this point. That obviously does not apply to this hypothetical estate with a $20,000 checking account. A handful of states also impose inheritance taxes, but we won't deal with that here.

As noted above, your aunt's will left her entire estate to you and your two siblings in equal shares. In the journal you record each distribution as a separate entry:

        2017/12/15 distribution to me
            distributions                      6544.34
            assets:estate checking            -6544.34

        2017/12/15 distribution to brother
            distributions                      6544.33
            assets:estate checking            -6544.33

        2017/12/15 distribution to sister
            distributions                      6544.33
            assets:estate checking            -6544.33

Now you run a final balance to make sure there's nothing left in the estate:

        $ hledger balance  
                      367.00  disbursements
                       60.00    administration
                      150.00    court costs
                      157.00    debts
                    19633.00  distributions
                   -20000.00  inventory
        --------------------
                           0

As you can see, neither ``assets`` nor ``estate checking`` appear because they each have a zero balance. If you want to show the zero-balance accounts--just to clearly illustrate the estate has no assets remaining--then include the flag ``-E`` with the ``hledger balance`` command:

        $ hledger balance -E
                           0  assets
                           0    aunt's checking account
                           0    estate checking
                      367.00  disbursements
                       60.00    administration
                      150.00    court costs
                      157.00    debts
                    19633.00  distributions
                   -20000.00  inventory
        --------------------
                           0

## What's Next?

Again, this was a very simple overview of the probate accounting process. In the next series of posts, I'll go into more detail about how to inventory an estate, addressing in greater detail the valuation of different types of assets. I'll also explain how to properly distinguish probate from non-probate assets.
