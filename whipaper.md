# Aletheia - Inflation Oracle whitepaper
version: `paper_napkin`  

last edit: August 29th, 2021  

Author: Odysseas Lamtzidis  

project: Aletheia project  

GitHub: https://github.com/OdysLam/aletheia  

Presentation: https://docs.google.com/presentation/d/13rXXzi_Ylf82l2iisFeCouU27wr7G7mnJsaoeXFMGAo/edit#slide=id.p  

![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FSymposium%2F_EpcFMNnvv.png?alt=media&token=23a582ba-f7b6-49cf-adb6-825550e9a476)  

**Disclaimer**  

To say that the project is under heavy development, it would be an understatement. The project is still under "heavy definition", meaning that there are multiple open questions and areas to research. That's good. We want as many known unknowns as possible.   

# Introduction  

It's an Oracle. It accurately measures the national inflation of any country. It's based on sound research that started in Harvard and MIT.   

Inflation is important, as it accurately shows the true wealth that society has. It's no good to be a billionaire, if you live in Zimbabwe[*][The 1 billion Zimbabwe dollar bill](https://www.banknoteworld.com/zimbabwe-currency/1-billion-zimbabwe-dollars/). Accessed at July 4th, 2021.).  

> The end game of rampant inflation is always war and/or revolution. Show me a regime change, and I will show you inflation. When you work your ass off only to stand still or get poorer, any “ism” that promises affordable food and shelter for the unwashed masses will reign supreme. If you are starving to death, nothing else matters except feeding your family. The symptoms of inflation are populism, social strife, food riots, high and rising financial asset prices, and income inequality. (..) Invest wisely and you can maintain or increase your standard of life against the rising fiat cost of energy. Invest poorly and the road to serfdom is real. You will find yourself working harder for a declining standard of living, and your fiat earnings and assets will not be able to keep up with the rising fiat cost of energy." — [Arthur Hayes](https://blog.bitmex.com/pumping-iron/)  

It's an important information to have about our society, but thus far it was only reported via centralised, governmental agencies. This is flawed, as the government has an incentive to lie about the real inflation, in an effort to hide bad policies. A decentralized inflation oracle gives the tools to the people to run their own oracle and measure the inflation themselves. Moreover, as we are talking about an oracle, this information can be safely be inserted as a blockchain, as an indisputable fact of reality. Finally, this financial data point enables us to build DeFi products that are based on the level of inflation, opening the door for inflation-adjusted securities on-chain.  

# State of The Art (WIP)  

## Oracles  

### Chainlink  

Chainlink([14][Chainlink](https://chain.link/). Accessed at June 28th, 2021)) is a decentralized network of nodes that provide data and information from off-blockchain sources to on-blockchain smart contracts via oracles.  

A Chainlink network is made up of a collection of Chainlink nodes with registered Job specifications, who can carry out Jobs execution coordinated by the on-chain Oracle contract(s), which use LINK Tokens as an incentive for the Chainlink node operators to serve clients via the Chainlink client smart contracts. Although we should go into more detail about the broad mechanism design of Chainlink, the reason we opted not to pursue integration with the service can be succinctly described as follows. Although it's a great project, it's not decentralized enough but uses reputation and a trusted setup to work properly. We want a system where complete decentralization is possible, where a DAO (and thus its governance token holders) have the power to decide on the parameters of the system and its players. In this use case, the players are the data feeds that participate in our Oracle. The same line of thought is used by MakerDAO's Oracle Lead[*]Niklas Kunkel, 2020. ["ChainLink Oracles for LINK-USD"](https://forum.makerdao.com/t/using-chainlink-oracles-for-link-usd/2670/21). Post number 21.  Accessed at June 28th, 2021), when he advocated for not using Chainlink as an Oracle in place of their own. The lack of crypto-economic security has also been described by Eric Wall in a relevant blog post[*]Eric Wall, 2021. ["What’s Wrong With the Chainlink 2.0 Whitepaper? (For Simpletons)"](https://ercwl.medium.com/whats-wrong-with-the-chainlink-2-0-whitepaper-for-simpletons-d50f27049464). Accessed at June 28th, 2021).  

### makerDAO  

MakerDAO is a decentralized organization built on Ethereum to allow lending and borrowing of cryptocurrencies without the need for a middle man. It's made up of a smart contract service that manages borrowing and lending, as well as two currencies: DAI and MKR to regulate the value of loans. Most cryptocurrency assets are volatile, the amount someone borrowed in crypto and the amount someone had to pay back could be wildly different over a short period of time. By combining loans with a stable currency, MakerDAO wants to allow anyone to borrow money and reliably predict how much they had to pay back.  

Our interest with MakerDAO is dual. On one hand, it's a model DAO that backs a cryptocurrency with specific attributes. The way it functions and it manages to keep the value of it's currency stable, will be used as a template for us to build on top of the inflation Oracle.    

MakerDAO has a very interesting Oracle[*][MakerDAO oracles-v2 GitHub repository](https://github.com/makerdao/oracles-v2), accessed at June 28th, 2021) implementation, which we will describe, as it served as an inspiration for the design choices that we took. The oracle agents talk off-chain in a p2p fashion, gossiping the values that they gather. Thus, under normal operation and without significant network issues, all agents are aware of all agent's data feeds. Some agents may run an additional program, which is called the "Relayer" and is responsible for grouping together the values from these feeds and submitting the data to the Oracle smart contract. In short, the current implementation has 2 modules:  

[Feed] Each Feed runs a Feed client which pulls prices through Setzer, signs them with an ethereum private key, and broadcasts them as a message to the secure scuttlebutt network. Setzer is a service, developed by MakerDAO, that reads API endpoints from various known exchanges.  

[Relay] Relays monitor the gossiped messages, check for liveness, and homogenize the pricing data and signatures into a single ethereum transaction.  

The smart contract then takes the median value of the submitted values and considers that value to be the "view" of the MakerDAO system for the world. The value is submitted with a considerable delay so that the DAO has time to react in case of Oracle's malicious action.  

Currently the Oracle system works with a quorum requirement. For a price to be updated, 13 out of 25 Oracle Feeds must submit data[*]Niklas Kunkel, 2020. ["ChainLink Oracles for LINK-USD"](https://forum.makerdao.com/t/using-chainlink-oracles-for-link-usd/2670/21). Post number 21.  Accessed at June 28th, 2021).  

The agents must be whitelisted in order to participate in the system, a process that is conducted through the Governance process of makerDAO. The oracles are ran by organisations and reputable individuals of the community. While the organizations are known, only 2 of the individuals are.   

### Provable  

A service that offers Oracle services for various blockchains. Although known and proven, it's a centralised  solution.   

### Tellor  

https://www.tellor.io/  

TBD  

### Witnet  

## DAOs  

TBD  

## DeFi products, platforms  

TBD  

### Rebasing Tokens  

Ampleforth  

Lido  

# Inflation  

## What is inflation   

https://www.lynalden.com/inflation/  

https://www.taxresearch.org.uk/Blog/2021/03/14/why-inflation-is-not-a-threat/  

https://blog.bitmex.com/pumping-iron/  

https://books.google.gr/books?hl=en&lr=&id=u8TiBwAAQBAJ&oi=fnd&pg=PT6&dq=inflation+history&ots=aCe_wcNnGm&sig=qM5s7PDdVHAleKO9RP8L-I8dTpc&redir_esc=y#v=onepage&q=inflation%20history&f=false  

CAMPBELL, JOHN Y., ROBERT J. SHILLER, and LUIS M. VICEIRA. "[Understanding Inflation-Indexed Bond Markets](https://www.nber.org/system/files/working_papers/w15014/w15014.pdf)." _Brookings Papers on Economic Activity_ 2009 (2009): 79-120. Accessed July 2, 2021. http://www.jstor.org/stable/25652715  

  

TBD  

## Why Inflation is important  

https://www.bloomberg.com/news/articles/2021-03-01/inflation-2021-malnutrition-and-hunger-fears-rise-as-food-prices-soar-globally  

TBD  

## Inflation concepts  

https://books.google.gr/books?hl=en&lr=&id=2TxbDwAAQBAJ&oi=fnd&pg=PP1&dq=inflation+&ots=AOskMnt-7y&sig=fIoF-M2LAo_qdCmo25gCYa5BvCM&redir_esc=y#v=onepage&q=inflation&f=false  

https://en.wikipedia.org/wiki/Inflation  

The references of this article  

TBD  

## How inflation is estimated now?  

https://www.jstor.org/stable/1991070  

TBD  

## Inflation Estimation using online prices  

### Formula  

The following points are _excerpts_ from the work[*]Cavallo, Alberto. ["Online and Official Price Indexes: Measuring Argentina's Inflation." ](https://www.hbs.edu/faculty/Pages/download.aspx?name=Cavallo%20Alberto%20J13.pdf)Journal of Monetary Economics 60, no. 2 (March 2013): 152–165.\) of Alberto Cavallo, who pioneered this methodology for gauging the inflation from the online prices of retailers.  

First, daily data are used to construct the online price indexes. Such high-frequency is useful to observe short-term patterns in the data that help validate the online information, although similar results can be obtained with monthly data.  

Second, the online indexes are built using prices for all products available for purchase at each retailer. This implies that the basket of goods changes dynamically over time as products appear or disappear from the online stores, and that the number of prices for product varieties tends to be much larger than in official statistics. Section 5.3.3 finds similar results<br/>when a fixed basket or alternative sub-samples of goods are used.  

Third, there are no forced product substitutions or adjustment for quality changes. All goods are treated independently, so products that are discontinued on a given date stop affecting the index from that day forward. Similarly, new goods only impact the index on their second day in the sample, when their first price change can be observed. This has no impact on the results that follow because these substitutions and quality adjustments are not common in official statistics for the categories of goods analyzed in this paper.  

Index computation  

1. To build the index, price changes are calculated at the product level, then averaged inside categories using unweighted geometric means, and finally aggregated across categories with a weighted arithmetic mean. In particular, the first step is to obtain the unweighted geometric average of price changes in category j for each day t:  

$$R^j_{t, t-1} = \prod_i( \frac{p^i_t}{p^i_{t-1}})^{1/n_{j,t}}$$, where $$p^i_t$$ is the price of good $$i$$ at time $$t$$, $$n_{j,t}$$ is the number of products in category $$j$$ that are present in the sample that day.  

2. The second step is to compute the category-level index at $$t$$.  

$$I^j_t=R^j_{1,0}*R^j_{2,1}*...R^j_{t,t-1}$$  

3. Finally, the supermarket Index is the weighted arithmetic average of all category indexes  

$$S_t=\sum_j\frac{w^j}{W}I^j_t$$, where $$w^j$$ is the official CPI[*][Consumer Price Index Frequently Asked Questions](https://www.bls.gov/cpi/questions-and-answers.htm). Accessed at July 6th, 2021.) for that category and $$W$$ is the sum of all the weights includes in the sample.   

The classification of products and weighing of categories is one of the most complex parts of this process. In the original data, each product is linked to a web address (URL) that corresponds to the webpage where the product is located. These URLs group similar items together, into various levels of aggregation chosen by each supermarket. The number of URLs ranges from about 300–1000 in these retailers. The advantage of having URLs is that thousands of items can be easily classified into a set of standardized official categories so that their corresponding official weights wj can be used to obtain the aggregate Daily estimates for the monthly and annual inflation rates are also obtained. At any point in time, the monthly inflation rate computes the percentage change in the average index of the last 30 days with respect to the average of the previous 30 days.   

Compared to CPI statistics, these online indexes have an advantage in terms of frequency and the number of items sampled within each category. For example, in Argentina alone, there are prices for 781 different product varieties in the ‘‘Milk’’ category alone (this includes different brands and package sizes). The main disadvantage is that these online prices come from a single retailer in only one city. As discussed below, this can limit the ability of online indexes to match the short-term inflation dynamics. However, this problem is minimized in this case because these Latin American supermarkets have huge market shares.  

  

# Inflation adjusted Securities  

TBD  

## Why inflation-adjusted securities  

In December of 2018, T.I.P.S. accounted for 9 percent of the federal debt held by the public, or more than $1 trillion. While inflation is low now, people perceive that there remains a risk it could rise, which has sustained a strong market for those bonds[*]Robert J. Shiller. [The Next New Thing in Finance — Bonds Linked Directly to the Economy](https://www.nytimes.com/2018/05/11/business/the-next-new-thing-in-finance-bonds-linked-directly-to-the-economy.html),  The New York Times, accessed at June 28th, 2021)  

Inflation is of the highest concern to normal people {[20]Robert J. Shiller, 1996. "[Why Do People Dislike Inflation?](https://ideas.repec.org/p/nbr/nberwo/5539.html)," [NBER Working Papers](https://ideas.repec.org/s/nbr/nberwo.html) 5539, National Bureau of Economic Research, Inc.)} and yet there is only one way to measure it. We have to trust the government, but they have an incentive to lie.  

The following are excerpts from the work[*]CAMPBELL, JOHN Y., ROBERT J. SHILLER, and LUIS M. VICEIRA. "[Understanding Inflation-Indexed Bond Markets](https://www.nber.org/system/files/working_papers/w15014/w15014.pdf)." _Brookings Papers on Economic Activity_ 2009 (2009): 79-120. Accessed July 2, 2021. http://www.jstor.org/stable/25652715) of John Y. Cambell, Robert J. Shiller, and Luis M. Viceira. The bolded emphasis is mine and doesn't appear in the original work.   

There are, however, two circumstances in which other assets can substitute for inflation-indexed bonds to provide long-term safe returns. First, if the breakeven inflation rate is constant, as will be the case when the central bank achieves perfect anti-inflationary credibility, then nominal bonds are perfect substitutes for inflation-indexed bonds, and conventional government bonds will suit the preferences of conservative long-term investors. For a time in the mid-2000s, it looked as if this nirvana of central bankers was imminent, **but the events of 2008 dramatically destabilized inflation expectations and reaffirmed the distinction between inflation-indexed and nominal bonds.**  

Second, if the ex-ante real interest rate is constant, as was famously asserted by Fama (1975)[*]Fama, Eugene, (1975), [Short-Term Interest Rates as Predictors of Inflation](https://econpapers.repec.org/RePEc:aea:aecrev:v:65:y:1975:i:3:p:269-82), _American Economic Review_, **65**, issue 3, p. 269-82.), then long-term investors can rollover short-term Treasury bills to achieve almost perfectly certain long-term real returns. Because inflation uncertainty is minimal over a month or a quarter, Treasury bills expose investors to minimal ináation risk. In general, they do expose investors to the risk of persistent variation in the real interest rate, but this risk is absent if the real interest rate is constant over time.  

A simple quantitative measure of the usefulness of inflation-indexed bonds is the reduction in long-run portfolio standard deviation that these bonds permit. We can estimate this reduction by calculating the long-run standard deviation of a portfolio of other assets chosen to minimize long-run risk. This is the smallest risk that long-run investors can achieve if inflation-indexed bonds are unavailable. Once inflation-indexed bonds become available, **the minimum long-run risk portfolio consists entirely of these bonds and has zero long-run risks**. Thus, the minimized long-run standard deviation of a portfolio of other assets measures the risk reduction that inflation-indexed bonds make possible.  

Long-term inflation-indexed bonds may be of interest to some short-term investors.<br/>Given their high short-run volatility, however, short-term investors will only wish to hold inflation-indexed bonds if they expect to receive high excess returns over Treasury bills (as might reasonably have been the case in 1999-2000, or during the<br/>yield spike of fall 2008), or if they hold other assets, such as stocks, **whose returns can be hedged by an inflation-indexed bond position**. We have shown evidence that TIPS and inflation-indexed gilts have hedged stock returns during the downturns of<br/>the early 2000ís and the late 2000ís, and this should make them attractive to short-term equity investors.  

## How Inflation-adjusted securities work  

The most used inflation adjusted security is  the Treasure Inflation-Protected Security or TIPS[*][Treasury Inflation-Protected Securities (TIPS)](https://www.investopedia.com/terms/t/tips.asp). Accessed at June 30th, 2021)  

Treasury Inflation-Protected Securities, or TIPS, provide protection against inflation. The principal of a TIPS increases with inflation and decreases with deflation, as measured by the Consumer Price Index. When a TIPS matures, you are paid the adjusted principal or original principal, whichever is greater.  

TIPS pay interest twice a year, at a fixed rate. The rate is applied to the adjusted principal; so, like the principal, **interest payments rise with inflation and fall with deflation.**  

# A Decentralised inflation oracle  

## Why is this important  

Because inflation is not always reported accurately, either because that the official bodies fail to respond to extraordinary events, such as the COVID crisis[*]Cavallo, Alberto. ["Inflation with COVID Consumption Baskets." ](https://www.hbs.edu/faculty/Pages/download.aspx?name=20-124.pdf)NBER Working Paper Series, No. 27352, June 2020. (Revised October 2020. Harvard Business School Working Paper, No. 20-124, May 2020)) or because it is in their best interest to falsely report the Inflation[*]Cavallo, Alberto, Guillermo Cruces, and Ricardo Perez-Truglia. ["Learning from Potentially Biased Statistics: Household Inflation Perceptions and Expectations in Argentina." (pdf)](https://www.hbs.edu/faculty/Pages/download.aspx?name=Cavallo_Alberto_J8_Learning%20from%20Potentially%20Biases%20Statistics.pdf) Brookings Papers on Economic Activity (Spring 2016): 59–108. ). The second is particularly important, as the Government has an incentive to lie about the real inflation. Of course, Argentina is not the only example of a country[*][Greece condemned for falsifying data](https://www.ft.com/content/33b0a48c-ff7e-11de-8f53-00144feabdc0). Accessed at July 3rd, 2021.) that falsified official statistics reports.  

The billion dollar prices project [*][The Billion Prices Project](http://www.thebillionpricesproject.com/), accessed at June 28th, 2021) that pioneered the computation of real inflation using online data, showed that it is possible for individuals to accurately measure the real wealth of a country. This is monumental, given the importance of the inflation in our daily lives and financial decisions.   

With a decentralized inflation oracle, there is a double goal:  

**Create a system where inflation is computed objectively and without bias.** Give the tools to people to measure and surface the true wealth, without having to blindly follow official statistics. In essence, make an open-source version of the billion-dollar price projects that anyone can run.  

**Make the inflation, as a data point, available in the blockchain**. That has remarkable implications. First, we transform the data point into an indisputable fact, it can't change once it's in there. Second, we can create DeFi products on top of that.   

A naive idea is to create a stablecoin that is inflation-adjusted, meaning that it's value is pegged to ~$1, but the amount a user has fluctuates so that the "real value" remains constant.  This is explored in Beta -- Inflation Adjusted DeFi.  

## Why Inflation-Adjusted DeFi  

TBD  

## Inflation estimation methodology  

It's an Oracle. It accurately measures the national inflation of any country. It's based on sound research that started in Harvard and MIT.   

Index computation  

1. To build the index, price changes are calculated at the product level, then averaged inside categories using unweighted geometric means, and finally aggregated across categories with a weighted arithmetic mean. In particular, the first step is to obtain the unweighted geometric average of price changes in category j for each day t:  

$R^j_{t, t-1} = \prod_i( \frac{p^i_t}{p^i_{t-1}})^{1/n_{j,t}}$, where $p^i_t$ is the price of good $i$ at time $t$, $n_{j,t}$ is the number of products in category $j$ that are present in the sample that day.  

2. The second step is to compute the category-level index at $t$.  

$I^j_t=R^j_{1,0}*R^j_{2,1}*...R^j_{t,t-1}$  

3. Finally, the supermarket Index is the weighted arithmetic average of all category indexes  

$S_t=\sum_j\frac{w^j}{W}I^j_t$, where $w^j$ is the official CPI[*](3s6fbvTfR) for that category and $W$ is the sum of all the weights includes in the sample.   

  

Thus, we have:  

Price Change: An R value, per item, per time unit  

Category-level index: A I value, per category, per time unit  

A supermarket Index: A S value, per retailer, per time unit  

Based on data obtained by prior work[*]Cavallo, Alberto. ["Scraped Data and Sticky Prices." ](https://www.hbs.edu/faculty/Pages/download.aspx?name=Cavallo_Alberto_J4_Scraped%20Data%20and%20Sticky%20Prices.pdf)Review of Economics and Statistics 100, no. 1 (March 2018): 105–119.) for the United States, we can make the following data stipulations:  

Data:  

10.2 million observations over 827 days. That's about 12.334 observations per day.  

30.000 products  

22 Categories  

241 URLs  

1 Retailer  

This produces:  

12.334 price changes $$R^j_{t, t-1}$$ per day  

12 $$I^j_t$$ category-level indexes per day  

1 Retailer Index $$S_t$$ per day  

For the Unites States, there are ample statistics available regarding the national CPI indexes ([*][Consumer Price Index](http://www.econport.org/content/handbook/Inflation/Price-Index/CPI.html). Accessed at July 6th, 2021.) and [**][Archived Relative Importance of Components in the Consumer Price Indexes](https://www.bls.gov/cpi/tables/relative-importance/home.htm#Archived%20Relative%20Importance%20Data). Accessed at July 6th, 2021.)).  

The index is created by the Retailer indexes, thus this is the final value that is output by the Oracle and made available inside the blockchain.  

Based on comments from [Alberto et al.]Cavallo, Alberto. ["Online and Official Price Indexes: Measuring Argentina's Inflation." ](https://www.hbs.edu/faculty/Pages/download.aspx?name=Cavallo%20Alberto%20J13.pdf)Journal of Monetary Economics 60, no. 2 (March 2013): 152–165.\), when choosing the Supermarket, we will need to choose an adequately large supermarket chain, that it has a considerable percentage of the market. This will reflect the nation-wide accuracy of it's prices. Moreover, multiple supermarkets will offer an even more accurate view of the situation.  

There is available data: http://www.thebillionpricesproject.com/datasets/  

That means that we can use the data set as a template to define categories and URL scraping targets.   

# Mechanism Design  

## Overall Design - Overview  

High level diagram of the 3 layers of the system and how they interact with one another, broad.  

## Mechanism Design for a Decentralised Oracle  

- [ ] open question: The following subjects need to be addressed.  

The mechanism for the Decentralized Oracle Governance.  

The mechanism around the reward/punishment of feeds based on their accuracy  

The mechanism around whitelisting(or not) feeds to participate in the Oracle  

What parts of the oracle will be designed to be modifiable?  

Attributes only (e.g Inflation Taxonomy)  

Certain functionality using proxy framework for upgradeability[*][Upgrading smart contracts](https://docs.openzeppelin.com/learn/upgrading-smart-contracts). Accessed at July 6th, 2021.)  

The Oracle will work via   

## Mechanism Design for an Inflation Adjusted Securiity  

TBD  

# Reference Design  

### Architecture - Feed Agent  

The MVP version of the oracle is a single Feed agent. A program that scrapes targets and accurately computes the inflation index, based on the Inflation estimation methodology.  The feed's architecture can be described as follows:  

**Aletheia (Rust agent) - Container**  

The agent will be written in Rust, a system programming language that has been rising in popularity over the last years. It's memory-safe and high-performance. The agent is compromised of modules, each module handling a particular function of the agent. The modules, in turn, can support any number of add-ons.   

The add-ons are part of the agent, but usually have to do with a particular interface or technology. For example, the **hermes** uses an HTTP add-on, as it needs to download websites over the HTTP protocol.  

The agent will run on a container, which abstracts the OS layer, enabling the Feed to run on *any* operating system that supports container virtualization. Moreover, by compiling the rust agent for different CPU architectures, it will be possible for the agent to run on different computer systems all-together, from Aarch64 to x64.  

This is a reference architecture, aiming to create a simple proof of concept.   

![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FSymposium%2FaKBKxn6t45.png?alt=media&token=7a131e72-058c-42eb-ab64-93f2adfcc58e)  

**hermes**  

It's the scraping module. Given a URL and an identifier (e.g [css selector](https://www.w3schools.com/cssref/css_selectors.asp)), it returns the corresponding value.    

**lethe**  

The archiver is responsible for compressing and archiving the raw data in a verifiable manner. The data is supplied by the **hermes**.  

Implementation Details:  

The **lethe** uses some already well-established platform for decentralised storage  of data. Such as Arweave[*][Arweave](https://www.arweave.org/). Accessed at July 2nd, 2021) or IPFS[*][IPFS](https://cloudflare-ipfs.com/ipns/ipfs.io/). Accessed at July 3rd, 2021.).  

 Based on data obtained by prior work[*](Rjg2RGCax) for the United States, we can make the following data stipulations:  

For about ~13.000 price changes per day and based on `csv` size estimations[*][Approximating data set csv size](https://www.stata.com/support/faqs/data-management/approximating-dataset-size/). Accessed at July 5th, 2021), we can safely assume a ~`1.2MB-2MB` `csv` file per day.   

For a year's data, the overhead is about `680MB`.  

The **lethe** **must** store the data in a way that ensures _availability_, so that an arbitrary agent (e.g an inflation index consumer) can verify the computations at any time.    

- [ ] open question **lethe** mechanism of permanently storing the raw data has implications for the overall incentive mechanism. This is mostly discussed in Mechanism Design for a Decentralised Oracle.  

**hephaestus**  

the comp is responsible for taking the raw values provided by the **hermes**  and computing the 1 Retailer Index $S_t$ per day.   

It simply implements the formula described in Inflation estimation methodology  

**eunomia**  

The identifier is responsible for managing the ID of the feed agent.  

- [ ] open question: What ID system will be used, something like **Urbit**[*](Rou-_AOLf) that has artificial scarcity or a simple Public/Private key scheme? It has implications in the Mechanism Design for a Decentralised Oracle.  

**Additional data point**: Urbit has an artificial scarcity, as there are about 4B different identities in total. Currently, a planet costs[*][Urbit.live marketplace](https://urbit.live/buy). Accessed at July 2nd, 2021) about ~$100 and a star ~$8.000. Urbit's ID system is succinctly described in **Urbit**[*](Rou-_AOLf).  

**aether**  

The ethereal is responsible for managing the feed's relationship with the Ethereum blockchain. It basically performs read/write operations to the blockchain.  

**optional modules**: Depending on Architecture -  Feed and Oracle connection these modules may or may not be required.   

**nemesis**  

The prover is responsible for creating proofs for the for computations that **hephaestus** did.   

- [ ] open question Given that the feed will store the original data via **lethe**, it shouldn't be required to produce proofs for it's computations. Users can just find the raw data and verify themselves.   

corolorarry there should be an easy way for a user to add the raw data to a program and get the index as an output, to verify.  This verifier could even be an agent, that reads the raw data of various feeds and verify their submitted data against the raw. If they find something abnormal, they get a reward.   

Implementation Details:  

Given the simple nature of the computations, I envision being able to _easily_ produce zero-knowledge proofs, that the computation did happen. That way, any user can verify that the feed is being honest and is indeed computing the indexes (versus just interpolating).  

As described in Inflation estimation methodology, the computations are 2 products and a sum.   

  

**arbitrator**  

 If an off-chain consensus solution is adopted, feeds will need to coordinate and agree on which feed will aggregate the index packages and call Oracle's smart contract. The arbitrator is the module that will house the consensus logic.   

**zephyrus**  

The P2P module. It is responsible for sending and receiving packets from other feed agents that participate in the cluster.   

There are multiple options for the protocol and we could implement different protocols, in parallel. That would enable the feeds to communicate in a more robust manner, as each protocol will function as a failsafe for the others.  This is important, as prior experience has shown with MakerDAO's Oracle, when the main P2P protocol ( **Secure Scuttlebutt**[*](N2i0t-n0U) ) failed, causing an outage[*][MakerDAO 11/25/20 Oracle Outage Post-Mortem](https://forum.makerdao.com/t/11-25-20-oracle-outage-post-mortem/5547). Accessed at June 28th, 2021).  

### Architecture - P2P Protocols  

**Urbit**[*][Understanding Urbit](https://urbit.org/understanding-urbit/). Accessed at July 2nd, 2021)  

Urbit is two components: Urbit OS and Urbit ID. It's both a p2p network and a new OS. As an OS, it's a VM, a programming language and a kernel that is designed to run software for an individual. In the Urbit world, each person has their own OS node, or an urbit. Although there is some nuisance in the design of the urbit, as it deviates considerably from most traditional computing, what we mainly care about is it's networking layer and ID system  

Urbit ID is an identity and authentication system specifically designed to work with Urbit OS. When you boot or log in to Urbit OS, you use your Urbit ID. The ID is a short memorable name (e.g ~sipsen-pilser) and it's both a username, a network address, and a crypto wallet.   

Urbit has designed it's own p2p protocol, called Ames, build on top of UDP packets. Ames encrypts every message using symmetric-key encryption by performing an elliptic curve Diffie-Hellman using the private key of the sender and the public key of the receiver.   

Urbit IDs  are stored on the Ethereum blockchain, in a suite of smart contracts called Azimuth. In essence, it ties an Urbit ID with a particular set of network keys. To change your network keys, you will need to make a transaction and change the state of the Azimuth smart contract. Azimuth, functions as the Urbit's public-key infrastructure.  

Urbit's system has a hierarchy, meaning that there are galaxy identities, which in turn spawn star identities and each star spawn planet identities. Planets are meant to function as users, stars as ISPs, and galaxies as DNS servers. For now, packet relaying is handled entirely by galaxies. Every galaxy is responsible for knowing the IP and port of every planet underneath it. In the future, galaxies will only need to know the star sponsoring a planet, and stars will be responsible for the final step of the relay. Thus, when a planet sends a message to a planet, it first asks the star and then the galaxy, if they know the IP address of a particular planet. If they don't, the galaxy is responsible for asking the other galaxies, and so forth.   

Urbit is under heavy development by Tlon.  

**Implementation**  

A feed can easily use Urbit, without having to handle the complexity of its internal systems, via an HTTP API.  That means that an Urbit VM will have to run alongside the Agent Feed's process.  

In Urbit, only the receiver can read a message. The receiver can be a certain identity, but also a group of identities, so things like common feeds can be implemented.   

**Secure Scuttlebutt**[*][Scuttlebutt Protocol](https://ssbc.github.io/scuttlebutt-protocol-guide/). Accessed at June 28th, 2021)  

Secure Scuttlebutt(SSB) is a database protocol for unforgeable append-only message feeds.  

Scuttlebutt forms a global cryptographic social network with its peers. Each user is identified by a public key, and publishes a log of signed messages, which other users follow socially.   

Scuttlebutt searches the P2P mesh for new messages and files from followed users and from FoaFs (friend of a friend's). The messages and files are stored locally, indefinitely, for applications to read.  

In SSB the identities are long and random, meaning that a user can easily create a new one, in contrast with Urbit. It's like generating a new email address.Scuttlebutt is used by MakerDao's Oracle v2. Albeit's a serious technical bug that exists, it has been tested before in a relevant co  

Scuttlebutt is used by MakerDao's Oracle v2. Albeit's a serious technical bug that exists, it has been tested before in a relevant context.  

**Implementation**  

SSB doesn't currently have a rust library. We will need to use an external program[*][ssb-server](https://github.com/ssbc/ssb-server). Accessed at July 2nd, 2021) that will run in parallel with the rust agent. This program will be responsible for sending and receiving messages over the SSB network.   

All feeds will subscribe to the same SSB network, having access to all the messages that are broadcasted.   

**libp2p**[*][libp2p](https://cloudflare-ipfs.com/ipns/libp2p.io/). Accessed at July 2nd, 2021)  

It's a modular network stack by Protocol Labs, the same company behind IPFS and Filecoin.  

libp2p uses public-key cryptography[*][Public Key Cryptography - Wikipedia](https://en.wikipedia.org/wiki/Public-key_cryptography). Accessed at July 6th, 2021.)  as the basis of peer identity, which serves two complementary purposes. First, it gives each peer a globally unique “name”, in the form of a `PeerId`[*][libp2p PeerID](https://cloudflare-ipfs.com/ipns/docs.libp2p.io/reference/glossary/peerid). Accessed at July 6th, 2021. ). Second, the `PeerId` allows anyone to retrieve the public key for the identified peer, which enables secure communication between peers.  

There are many cases where we only have the PeerId for the peer we want to contact, and we need a way to discover their network address. Peer routing is the process of discovering peer addresses by leveraging the knowledge of other peers.  

The current stable implementation of peer routing in libp2p uses a distributed hash table[*][libp2p distributed hash table](https://cloudflare-ipfs.com/ipns/docs.libp2p.io/reference/glossary/dht). Accessed at July 6th, 2021.) to iteratively route requests closer to the desired PeerId using the Kademlia[*][Kademlia](https://en.wikipedia.org/wiki/Kademlia). Accessed at July 6th, 2021.) routing algorithm.  

**Implementation: **  

libp2p is implemented in many different languages[*][libp2p rust support](https://cloudflare-ipfs.com/ipns/libp2p.io/implementations/). Accessed at July 2nd, 2021). Rust support is adequate, as it supports basic p2p communication, encryption and routing.  

### Architecture -  Feed and Oracle connection  

The feed communicates with the Oracle, by calling a certain interface function on the Oracle's smart contract. There are 2 subjects of interest here:  

1) What data is passed to the **aggregator** smart contract?  

2) Which feeds call the smart contract  

Let's answer them in order.  

### Data input to aggregator  

Ever feed F supplies:  

```javascript
int epoch
mapping(string => int) retailerIndexes
string rawDataLocationHash
string computationProof```  

### Feed calls to Oracle Smart contracts  

There are different ways to do this:  

Every feed $$i$$ calls the smart contract to register their Package $$P_i^e$$ for epoch e.  

Feeds agree off-chain on which feed will aggregate the packages $$P_i^e$$, for every $$i$$ and make the smart contract call that will contain the set $${P_1^e, P_2^e,...P_k^e}$$, where k is the number of feeds.  

No "official" inflation index, but a list of different inflation indices by different players. User has the freedom to choose to follow whichever feed is deemed more accurate (reputation based).  

There is an important note here, and that has to do with how the  **gifter** works. We have defined that feeds are being rewarded based on the difference between the value they submitted and the median that was chosen by the Oracle. This has a very important requirement: The submitted values must be revealed simultaneously, else a feed could simply read the blockchain and copy another feed's values.  

A **naive approach** would be to have a commit-reveal framework, where feeds first submit a commitment to the package they will submit (e.g the keccak256 hash of the package). The commitment does not reveal anything about the value to be submitted. Afterwards, they  submit the package itself and the smart contract can easily verify if the package and the hash are correct.  

This note affects the possible solutions that we will briefly explore next.  

- [ ] open question There are different MEV implications in regard to how we choose to handle the Feed/Oracle connection.    

### Possible solutions  

- [ ] open question What is the best solution for the decentralized oracle?   

**Solution 1: **A8FMm5hsX  

**Solution 2: **ZwHLqiysP  

![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FSymposium%2FtATXtAjQ70.png?alt=media&token=2f072850-7dc6-455d-bf09-4e30efec6fde)  

**Solution 1: **Every feed $i$ calls the smart contract to register their Package $P_i^e$ for epoch e.  

Given [how the reward system - gifter works]There is an important note here, and that has to do with how the gf_GMJygP works. We have defined that feeds are being rewarded based on the difference between the value they submitted and the median that was chosen by the Oracle. This has a very important requirement: The submitted values must be revealed simultaneously, else a feed could simply read the blockchain and copy another feed's values.), every feed will need to produce 2 transactions in 2 distinct phases, in a commit-reveal scheme.   

Given  L2 scaling solutions, such as rollups, this system could work with minimal cost.   

Pros:  

Reduce complexity from the mechanism design, as we don't need the feeds to communicate with a P2P fashion. Each interacts with the Oracle on it's own. The oracle is responsible for "organizing" the commit/reveal phase.  

Cons:  

If we stick with L1, this could produce a daily non-negligible transaction cost of 2 transactions per day per feed.  

- [ ] open question: What are the a) security, b )mechanism design, and c) MEV implications if the mechanism requires an L2 solution?  

**Solution 2: **Feeds agree off-chain on which feed will aggregate the packages $P_i^e$, for every $i$ and make the smart contract call that will contain the set ${P_1^e, P_2^e,...P_k^e}$, where k is the number of feeds.  

Feeds communicate with each other, through the **zephyrus** module, via some P2P protocol, as discussed in Architecture - P2P Protocols. The coordinate so that a feed is responsible to aggregate the packages from all the feeds and make the transaction that will submit the packages to the Oracle.  

**Pros:**  

The sunny-day scenario (meaning no attack) will have a single transaction/day.  

Due to the extremely low transaction frequency, there is no requirement for L2 solutions.  

Incentives can be baked into the Oracle, trivially, to reward the Leader.   

This is the solution adopted by Maker Oracle-v2, thus there is prior work in this field.  

It seems that Chainlink is moving in this direction([*]Alex Coventry, 2019.[Threshold Signatures in Chainlink](https://blog.chain.link/threshold-signatures-in-chainlink/). Accessed at July 3rd, 2021.), [**][Hybrid smart contracts explained](https://blog.chain.link/hybrid-smart-contracts-explained/). Accessed at July 3rd, 2021.)), where data feeds coordinate before relaying information to the blockchain.   

Multiple projects moving towards a particular direction is signal that it may be the right path.  

**Cons:**  

It adds considerable complexity, as we need to design a system for the nodes to come into agreement regarding the leader. The complexity concerns:  

An off-chain mechanism design and it's threat model  

The implementation of the P2P connectivity  

- [ ] open question:   

1) Do we need a consensus amongst feeds on which feed will make the smart contract call? The alternative would be that **any** feed can aggregate packages and try to call the smart contract first. Only one will succeed. This is different to [Solution 1]**Solution 1: **A8FMm5hsX) where every Feed calls the smart contract to submit **only their package**.  

2) If we need a consensus: What is the best way to achieve an off-chain consensus? Could we model this as permissioned, separate blockchain where feeds are the block producers?  

This is done by Tellor.   

**Additional data points**: Based on a forum post[*]Niklas Kunkel, 2021.[Response to ChainLinkGod Accusations](https://forum.makerdao.com/t/response-to-chainlinkgod-accusations/9112). Accessed at July 3rd, 2021) in the MakerDAO forum, it appears that the architecture for Oracle v2 does not require consensus amongst feeds on who will update the Oracle. Any feed may run a "relayer" program, which is responsible for aggregating data from all the feeds (by listening to the common feed channel) and "relaying" the information to the oracle. It is unclear what happens when several relayers are running in parallel, as it would create a race condition where only 1 relayer succeeds and the others fail.   

**Solution 3:** No "official" inflation index, but a list of different inflation indices by different players. User has the freedom to choose to follow whichever feed is deemed more accurate (reputation based).  

A reputation-based system. Every feed has a unique identity and the smart contract simply serves as a registry.  

Users can elect to follow whichever feed they want, based on reputation. Given that original data are published, users can validate and find improper players. In particular, feeds have an incentive to find and signal that another feed is not right. A platform can enable the communication between users and feeds, as also how users can reimburse feeds for their services.   

### Architecture - Oracle   

The architecture of the Oracle follows that of MakerDAO, with a few additions, namely the   **gifter** and **mesa** modules.  

The Oracle is a set of smart contracts:  

**aggregator**  

Aggregating the data from the feeds and defining the oracle's view of the world.  

Implementation detail:  

The aggregator follows MakerDao's structure of the Oracle-v2 Medianizer.   

For gas efficiency, it could expect a sorted array of feed's values and then it picks the median value (the one in the middle). The value is made available to the **security** module.   

There are other ways to do it (e.g implement a quick-sort algorithm)  

**security**  

Securing the Oracle against malicious activity:  

a) Add a delay to the Oracle's feed update, so that there is time to response against an attack  

b) Verify the ID of the ethereum address that call Oracle's interfaces  

Implementation detail:  

The aggregator follows MakerDao's structure of the Oracle-v2 OSM module.   

With every epoch, it gets an update by the **aggregator**. With every update, it makes the previous epoch's value available to the rest of the system. In other words, the system has a full epoch (a day) to deal with a bad input to the system.   

**concierge**  

Making available the Oracle's value for other smart contracts to use.  

**mesa**  

Define various attributes of the Oracle:  

Target URLs   

Inflation taxonomy (retailer, country, product category, CPI weights)  

Whitelisted ethereum addresses to use the Oracle  

Whitelisted ethereum addresses that can change the various attributes of the Oracle  

Feed rewards  

Implementation details:  

Inflation taxonomy (retailer, country, product category, CPI weights)  

Storing on the blockchain is an expensive operation. Depending on the number of distinct URLs, we may follow 2 different ways: a) store everything on-chain or b)use a decentralized storage solution and store the `location_hash` in the contract.  

a) The implementation is obvious.  

b) For this solution, we could use something like IPFS[*][IPFS](https://cloudflare-ipfs.com/ipns/ipfs.io/). Accessed at July 3rd, 2021.), but we would need a whole new range of incentives for people to ensure the availability of the data. An easier solution is to use Arweave[*][Arweave](https://www.arweave.org/). Accessed at July 2nd, 2021), a blockchain network with the purpose of storing data, forever.   

 Although an analysis of that system's design is out of the scope (at least for version: `paper_napkin`), we can succinctly say that it's based on the assumption that storage will continue to get cheaper. Thus, if I pay upfront for the storage, based on current prices, the storage provider will pocket the storage cost reduction that we assume will come in the future.  

**Naive solution:**   

Store the data described in Data structures that are required by the feed to start scraping. as a `csv` file on arweave and then "anchor" the data's location using the `location_hash`. The feeds will simply need to read the `hash` from the smart contract's storage and fetch the file from the Arweave network.   

In the decentralized Oracle's environment, the Governance can change the file, by simply uploading a newer version and changing the hash stored in the smart contract.  

- [ ] open question: What are the security implications of using Arweave?  

Data structures that are required by the feed to start scraping.  

```javascript
{"retailer": "country"}
{"product_id": "CPI_product_category"}
{
  "urls":["
         {
         "product_id": "identifier"
          "identifier_type": "css_selector" || "regex"
         }"
		]
}
{"CPI_product_category": "CPI_weight" }```  

The identifier is the unique element that will be used to find the price for that particular product item. A `css selector`, a `regex` expression, etc.  

Whitelisted ethereum addresses to use the Oracle  

A simple `address[]` of ethereum addresses that can call the Oracle and read it's values  

Whitelisted ethereum addresses that can change the various attributes of the Oracle  

A simple `address[]` of ethereum addresses that can call smart contract functions that change attributes of the Oracle.  

Feed rewards  

The base feed reward, an `int`.  

 **gifter**  

Reward Feeds for their services based on the formula. The gifter :  

Computes the rewards for each feed  

Sends the reward to the feed's address. The reward is made available from Oracle's treasury, which will be funded and managed by **mesa**  

Formula  

**Naive Approach**: Use Euclidean distance[*][Euclidean Distance](https://en.wikipedia.org/wiki/Euclidean_distance). Accessed at July 2nd, 2021) from the Median and a base reward.  

Euclidian Distance: $$d(p,q) = \sqrt{(p-q)^2} $$, where $$p$$ is the median index chosen by the **aggregator** and $$q$$ is the index supplied by the feed.  

Reward $$R_i = T - d_i$$. If $$R_i<0$$, then $$R_i=0$$. Where $$T$$ is a threshold value set by the Oracle and $$R_i$$ is reward for Feed $$i$$.  

- [ ] open question: Consider an alternative rewarding mechanism where the reward is a zero-sum game between the feeds.  

Given the decentralized nature of Oracle, we expect that **Mesa** will interface with a DAO, which will be able to change Oracle's attributes via its governance process. The architecture of the DAO will be defined in later iterations of the project, as the Architecture - Inflation Adjusted DeFi is refined.  

### Architecture - Inflation Adjusted DeFi  

TBD  

# Roadmap  

## MVP -- Inflation feed   

### Feed Agent -- MVP  

Gathers price data  

Compute inflation index  

Archive raw data  

Feeds an arbitrary feed with said inflation data.   

An interesting approach and possible way to fund the project is to use bitclout[*][Bitclout](https://bitclout.com/). Accessed at July 2nd, 2021) as the first feed module. The idea is that it feeds a bitclout account with a daily inflation feed. People can speculate on the feed by buying the feed's creator coin, a native cryptocurrency of the bitclout platform. As the feed is providing an accurate and reliable service, so its creator's coin will rise and will create revenue to fund it's further development.   

At a high level, the following diagram shows the activities that the agent will perform.  

![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FSymposium%2FrHFjefSpYz.png?alt=media&token=f22f93c5-e949-4b1e-8ea7-35985f2c3982)  

`decentralized_storage_1` is the location hash that is defined in **mesa** smart contract in the version: Alpha -- Decentralised Oracle  

`decentralized_storage_2` is described in greater detail in the section we talk about the **lethe**.  

We can view the agent as a system with the following output at every epoch $$e$$:  

```javascript
{
  "inflationIndexes":[
    {
      "retailer1": int, 
      "retailer1Proof": string,
      "rawDataLocationHash": string,
      "rawDataLocationHashProvider": "arweave"
    }
  ],
   "epoch": timestamp
   "feedIdentities": {"ethereum": address, "urbit": string, "scuttlebut": string, "libp2p": string, ...}
}```  

## Outcomes  

Feed Agent -- MVP  

Whitepaper  

## Alpha -- Decentralised Oracle  

The alpha version is about using the MVP's agent to create a decentralized version of that Oracle feed. That means:  

Multiple Feed Agent -- MVP gather inflation data, they coordinate and reach a consensus off-chain, regarding which Feed will send aggregated data to the Oracle's smart contracts.  

A set of smart contracts create an Oracle entity on the Ethereum blockchain. That entity:  

Receives data from the Feeds and computes the inflation data point that will be made available in the blockchain  

Defines the taxonomy and URL locations to be scraped.  

Can change certain attributes of the Oracle via an admin interface  

That admin interface is controlled by a proto-DAO entity that may or may now support Governance tokens. Governance tokens are a way for users to vote on Governance proposals.   

### Aletheia Feed -- Alpha  

Research + Implementation: **optional modules**: Depending on hxBgh2zp2 these modules may or may not be required.   

## Outcomes  

Aletheia Feed -- Alpha  

Architecture - Oracle   

Architecture -  Feed and Oracle connection  

## Beta -- Inflation Adjusted DeFi  

TBD  

### Team  

![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FSymposium%2Fn_YwzHBUl6.png?alt=media&token=1543f2a6-80aa-4023-a033-9b3975899e90)  

## Whitepaper sections TBD  

  

## Open Questions   

Open Questions are unknowns that have been detected and require further research. We strive to eliminate as many unknown unknown as possible, mapping the territory that we know we have to further research.  

  

## References  

Cavallo, Alberto. ["Scraped Data and Sticky Prices." ](https://www.hbs.edu/faculty/Pages/download.aspx?name=Cavallo_Alberto_J4_Scraped%20Data%20and%20Sticky%20Prices.pdf)Review of Economics and Statistics 100, no. 1 (March 2018): 105–119.  

Cavallo, Alberto. ["Online and Official Price Indexes: Measuring Argentina's Inflation." ](https://www.hbs.edu/faculty/Pages/download.aspx?name=Cavallo%20Alberto%20J13.pdf)Journal of Monetary Economics 60, no. 2 (March 2013): 152–165.\  

[The Billion Prices Project](http://www.thebillionpricesproject.com/), accessed at June 28th, 2021  

Cavallo, Alberto, and Roberto Rigobon. ["The Distribution of the Size of Price Changes." ](https://www.hbs.edu/faculty/Pages/download.aspx?name=Cavallo-Rigobon-Distributions.pdf)NBER Working Paper Series, No. 16760, September 2012.  

Cavallo, Alberto, and Roberto Rigobon. ["The Billion Prices Project: Using Online Prices for Inflation Measurement and Research." ](https://www.hbs.edu/faculty/Pages/download.aspx?name=Cavallo_Alberto_J7_The%20Billion%20Prices%20Project.pdf)Journal of Economic Perspectives 30, no. 2 (Spring 2016): 151–178.  

Cavallo, Alberto. ["Are Online and Offline Prices Similar? Evidence from Large Multi-Channel Retailers." ](https://www.hbs.edu/faculty/Pages/download.aspx?name=Cavallo_Alberto_J6_Are%20Online%20and%20Offline%20Prices%20Similar.pdf)American Economic Review 107, no. 1 (January 2017): 283–303.  

Robert J. Shiller. [The Next New Thing in Finance — Bonds Linked Directly to the Economy](https://www.nytimes.com/2018/05/11/business/the-next-new-thing-in-finance-bonds-linked-directly-to-the-economy.html),  The New York Times, accessed at June 28th, 2021  

[Treasury Inflation-Protected Securities (TIPS)](https://www.investopedia.com/terms/t/tips.asp), accessed at June 28th, 2021  

Stefania D’Amico, Don H. Kim, and Min Wei, 2013. [Tips from TIPS: the Informational Content of Treasury Inflation-Protected Security Prices](https://www.federalreserve.gov/pubs/feds/2014/201424/201424pap.pdf). Finance and Economics Discussion Series. Divisions of Research & Statistics and Monetary Affairs Federal Reserve Board, Washington, D.C.  

[MakerDAO oracles-v2 GitHub repository](https://github.com/makerdao/oracles-v2), accessed at June 28th, 2021  

[The Maker Protocol: MakerDAO's Multi-Collateral Dai (MCD) System](https://makerdao.com/en/whitepaper/). Accessed at June 28th, 2021  

Niklas Kunkel, 2020. ["ChainLink Oracles for LINK-USD"](https://forum.makerdao.com/t/using-chainlink-oracles-for-link-usd/2670/21). Post number 21.  Accessed at June 28th, 2021  

Eric Wall, 2021. ["What’s Wrong With the Chainlink 2.0 Whitepaper? (For Simpletons)"](https://ercwl.medium.com/whats-wrong-with-the-chainlink-2-0-whitepaper-for-simpletons-d50f27049464). Accessed at June 28th, 2021  

[Chainlink](https://chain.link/). Accessed at June 28th, 2021  

U.S Bureau of Labor Statistics. [Archived Relative Importance of Components in the Consumer Price Indexes](https://www.bls.gov/cpi/tables/relative-importance/home.htm#Archived%20Relative%20Importance%20Data). Accessed at June 28th, 2021  

[Scuttlebutt Protocol](https://ssbc.github.io/scuttlebutt-protocol-guide/). Accessed at June 28th, 2021  

[MakerDAO 11/25/20 Oracle Outage Post-Mortem](https://forum.makerdao.com/t/11-25-20-oracle-outage-post-mortem/5547). Accessed at June 28th, 2021  

[SSB state size bug](https://github.com/ssbc/ssb-server/issues/689). Accessed at June 28th, 2021  

Diego Ongaro and John Ousterhout. 2014. [In search of an understandable consensus algorithm](https://raft.github.io/raft.pdf). In _Proceedings of the 2014 USENIX conference on USENIX Annual Technical Conference_ (_USENIX ATC'14_). USENIX Association, USA, 305–320.  

Robert J. Shiller, 1996. "[Why Do People Dislike Inflation?](https://ideas.repec.org/p/nbr/nberwo/5539.html)," [NBER Working Papers](https://ideas.repec.org/s/nbr/nberwo.html) 5539, National Bureau of Economic Research, Inc.  

CAMPBELL, JOHN Y., ROBERT J. SHILLER, and LUIS M. VICEIRA. "[Understanding Inflation-Indexed Bond Markets](https://www.nber.org/system/files/working_papers/w15014/w15014.pdf)." _Brookings Papers on Economic Activity_ 2009 (2009): 79-120. Accessed July 2, 2021. http://www.jstor.org/stable/25652715  

[Treasury Inflation-Protected Securities (TIPS)](https://www.investopedia.com/terms/t/tips.asp). Accessed at June 30th, 2021  

[libp2p](https://cloudflare-ipfs.com/ipns/libp2p.io/). Accessed at July 2nd, 2021  

[libp2p rust support](https://cloudflare-ipfs.com/ipns/libp2p.io/implementations/). Accessed at July 2nd, 2021  

[ssb-server](https://github.com/ssbc/ssb-server). Accessed at July 2nd, 2021  

Fama, Eugene, (1975), [Short-Term Interest Rates as Predictors of Inflation](https://econpapers.repec.org/RePEc:aea:aecrev:v:65:y:1975:i:3:p:269-82), _American Economic Review_, **65**, issue 3, p. 269-82.  

[Understanding Urbit](https://urbit.org/understanding-urbit/). Accessed at July 2nd, 2021  

[Urbit.live marketplace](https://urbit.live/buy). Accessed at July 2nd, 2021  

[Bitclout](https://bitclout.com/). Accessed at July 2nd, 2021  

[Arweave](https://www.arweave.org/). Accessed at July 2nd, 2021  

[Euclidean Distance](https://en.wikipedia.org/wiki/Euclidean_distance). Accessed at July 2nd, 2021  

Niklas Kunkel, 2021.[Response to ChainLinkGod Accusations](https://forum.makerdao.com/t/response-to-chainlinkgod-accusations/9112). Accessed at July 3rd, 2021  

Cavallo, Alberto. ["Inflation with COVID Consumption Baskets." ](https://www.hbs.edu/faculty/Pages/download.aspx?name=20-124.pdf)NBER Working Paper Series, No. 27352, June 2020. (Revised October 2020. Harvard Business School Working Paper, No. 20-124, May 2020)  

Cavallo, Alberto, Guillermo Cruces, and Ricardo Perez-Truglia. ["Learning from Potentially Biased Statistics: Household Inflation Perceptions and Expectations in Argentina." (pdf)](https://www.hbs.edu/faculty/Pages/download.aspx?name=Cavallo_Alberto_J8_Learning%20from%20Potentially%20Biases%20Statistics.pdf) Brookings Papers on Economic Activity (Spring 2016): 59–108.   

[Greece condemned for falsifying data](https://www.ft.com/content/33b0a48c-ff7e-11de-8f53-00144feabdc0). Accessed at July 3rd, 2021.  

Alex Coventry, 2019.[Threshold Signatures in Chainlink](https://blog.chain.link/threshold-signatures-in-chainlink/). Accessed at July 3rd, 2021.  

[Hybrid smart contracts explained](https://blog.chain.link/hybrid-smart-contracts-explained/). Accessed at July 3rd, 2021.  

[IPFS](https://cloudflare-ipfs.com/ipns/ipfs.io/). Accessed at July 3rd, 2021.  

[The 1 billion Zimbabwe dollar bill](https://www.banknoteworld.com/zimbabwe-currency/1-billion-zimbabwe-dollars/). Accessed at July 4th, 2021.  

[Approximating data set csv size](https://www.stata.com/support/faqs/data-management/approximating-dataset-size/). Accessed at July 5th, 2021  

[Upgrading smart contracts](https://docs.openzeppelin.com/learn/upgrading-smart-contracts). Accessed at July 6th, 2021.  

[Consumer Price Index](http://www.econport.org/content/handbook/Inflation/Price-Index/CPI.html). Accessed at July 6th, 2021.  

[Archived Relative Importance of Components in the Consumer Price Indexes](https://www.bls.gov/cpi/tables/relative-importance/home.htm#Archived%20Relative%20Importance%20Data). Accessed at July 6th, 2021.  

[Consumer Price Index Frequently Asked Questions](https://www.bls.gov/cpi/questions-and-answers.htm). Accessed at July 6th, 2021.  

[Public Key Cryptography - Wikipedia](https://en.wikipedia.org/wiki/Public-key_cryptography). Accessed at July 6th, 2021.  

[libp2p PeerID](https://cloudflare-ipfs.com/ipns/docs.libp2p.io/reference/glossary/peerid). Accessed at July 6th, 2021.   

[libp2p distributed hash table](https://cloudflare-ipfs.com/ipns/docs.libp2p.io/reference/glossary/dht). Accessed at July 6th, 2021.  

[Kademlia](https://en.wikipedia.org/wiki/Kademlia). Accessed at July 6th, 2021.  

Alberto Cavallo, 2016.[The Billion Prices Project Using Online Prices for Inflation and Research](https://bfi.uchicago.edu/wp-content/uploads/Cavallo-1.pdf). MFM Conference - NYU  

## Quotes  

> The end game of rampant inflation is always war and/or revolution. Show me a regime change, and I will show you inflation. When you work your ass off only to stand still or get poorer, any “ism” that promises affordable food and shelter for the unwashed masses will reign supreme. If you are starving to death, nothing else matters except feeding your family. The symptoms of inflation are populism, social strife, food riots, high and rising financial asset prices, and income inequality. (..) Invest wisely and you can maintain or increase your standard of life against the rising fiat cost of energy. Invest poorly and the road to serfdom is real. You will find yourself working harder for a declining standard of living, and your fiat earnings and assets will not be able to keep up with the rising fiat cost of energy." — [Arthur Hayes](https://blog.bitmex.com/pumping-iron/)  

  
