
<!-- Find and Replace All [repo_name] -->
<!-- Replace [product-screenshot] [product-url] -->
<!-- Other Badgets https://naereen.github.io/badges/ -->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
<!-- [![License][license-shield]][license-url] -->


<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
	<!-- <li><a href="#license">License</a></li> -->
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->
## About The Project

This project is an app that sorts through historical trade data for Bitcoin on two exchanges: Bitstamp and Coinbase.  I then apply the three phases of financial analysis to determine if any arbitrage opportunities existed for Bitcoin.

### Built With

<!-- This section should list any major frameworks that you built your project using. Leave any add-ons/plugins for the acknowledgements section. Here are a few examples. -->

* [Python](https://www.python.org/)
* [Python CSV Reading/Writing](https://docs.python.org/3/library/csv.html)
* [Python pandas](https://pandas.pydata.org/)
* [Python matplotlib](https://matplotlib.org/)
* [Python conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html)
* [Python JupyterLab](https://jupyter.org/)

<!-- GETTING STARTED -->
## Getting Started

<!-- This is an example of how you may give instructions on setting up your project locally. To get a local copy up and running follow these simple example steps. -->
* You don't need Python. You can install Anaconda and JupyterLab normally just like any other application on your computer. Follow the instructions for Anaconda, ensure that its working, then install JupyterLab.

* I have placed Comments throughout the code so that you can follow the code and be able to replicate the app on your own. Also, so that you're able to contribute in the future :-)

### Prerequisites

<!-- This is an example of how to list things you need to use the software and how to install them. -->
A text editor such as [VS Code](https://code.visualstudio.com/) or [Sublime Text](https://www.sublimetext.com/)


### Installation

1. Clone the repo
   ```sh
   git clone https://github.com/AnaIitico/bitcoin_arbitrage.git
   ```

2. You don't need to install pip - Conda comes with pip and you can also use the command
    conda install 'package name'
   
3. Install Conda according to the instructions based on your operating system.
    For windows users you MUST use the Administrator PowerShell. Users with AMD Processors MUST use the Administrator PowerShell 7 (X64) version
  
    Once installed Conda has an Admin PowerShell version shortcut - look on your Start menu for it.
    This shortcut will prove very useful at times when you need to install other apps or make adjustments to your installation

    Once installed you will see (base) on your terminal
   
4. Activate Conda Dev environment
   ```sh
   conda activate dev
   ```
   You should now see (dev) on your terminal

5. Install JupyterLabs
   ```sh
   pip install jupyterlab

6. Run JupyterLab
   ```sh
   jupyter lab
   ```
   A browser window should open on localhost:8889/lab

<!-- USAGE EXAMPLES -->
## Usage

<!-- Use this space to show useful examples of how a project can be used. Additional screenshots, code examples and demos work well in this space. You may also link to more resources. -->
This project is an app that sorts through historical trade data for Bitcoin on two exchanges: Bitstamp and Coinbase.  I then apply the three phases of financial analysis to determine if any arbitrage opportunities existed for Bitcoin.

<!-- ROADMAP -->
## Roadmap

Here are some screenshots and code snippets of the working app

#### Exchange Comparison January 2018
![Exchange January Screen Shot][exchange-january-screenshot]

#### Exchange Comparison March 2018 - With Analysis
![Exchange March Screen Shot][exchange-march-screenshot]


#### Calculate Arbitrage Profits Snippet - for January 16 only
#### you can see the full code (with outputs) in the [crypto_arbitrage.ipynb](https://github.com/AnaIitico/bitcoin_arbitrage/blob/main/crypto_arbitrage.ipynb) file
  *This code has been summarized into one block for convenience*
  *and there's an analysis at the end*
```sh
  # For the date early in the dataset, measure the arbitrage spread between the two exchanges
  # by subtracting the lower-priced exchange from the higher-priced one
  arbitrage_spread_early=coinbase['Close'].loc['2018-01-16']-bitstamp['Close'].loc['2018-01-16']
  arbitrage_spread_early = arbitrage_spread_early[arbitrage_spread_early>0]
  # Use a conditional statement to generate the summary statistics for each arbitrage_spread DataFrame
  arbitrage_spread_early.describe()

  # For the date early in the dataset, calculate the spread returns by dividing the instances when the
  # arbitrage spread is positive (> 0) 
  # by the price of Bitcoin from the exchange you are buying on (the lower-priced exchange).
  spread_return_early=arbitrage_spread_early/bitstamp['Close'].loc['2018-01-16']
  # Review the spread return DataFrame
  spread_return_early.head()

  # For the date early in the dataset, determine the number of times your trades with positive returns 
  # exceed the 1% minimum threshold (.01) that you need to cover your costs
  profitable_trades_early=spread_return_early[spread_return_early>.01]
  # Review the first five profitable trades
  profitable_trades_early.head()

  # For the date early in the dataset, generate the summary statistics for the profitable trades
  # or you trades where the spread returns are are greater than 1%
  profitable_trades_early.describe()

  # For the date early in the dataset, calculate the potential profit per trade in dollars 
  # Multiply the profitable trades by the cost of the Bitcoin that was purchased
  profit_early=profitable_trades_early * bitstamp['Close'].loc['2018-01-16']
  # Drop any missing values from the profit DataFrame
  profit_per_trade_early=profit_early.dropna()
  # View the early profit DataFrame
  profit_per_trade_early

  # Generate the summary statistics for the early profit per trade DataFrame
  profit_per_trade_early.describe()

  # Plot the results for the early profit per trade DataFrame
  profit_per_trade_early.plot(figsize=(10, 7), title="Profit Per Trade - Jan 16")

  # Calculate the sum of the potential profits for the early profit per trade DataFrame
  profit_sum_early=profit_per_trade_early.sum()
  profit_sum_early

  # Use the cumsum function to calculate the cumulative profits over time for the early profit per
  # trade DataFrame
  cumulative_profit_early=profit_per_trade_early.cumsum()
  # Plot the cumulative sum of profits for the early profit per trade DataFrame
  cumulative_profit_early.plot(figsize=(10, 7), title="Cumulative Sum - January 16")

  #**Answer:** The profit information supports the trend in the narrowing of the spread
  #from January to March. As the spread narrows, so does the opportunity for profit,
  #as it is evident in the calculated results.
 ```

See the [open issues](https://github.com/AnaIitico/bitcoin_arbitrage/issues) for a list of proposed features (and known issues).

<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<!-- LICENSE -->
<!-- ## License

Distributed under the MIT License. See `LICENSE` for more information.
 -->

<!-- CONTACT -->
## Contact

Jose Tollinchi - [@josetollinchi][linkedin-url] - jtollinchi1971@gmail.com

Project Link: [https://github.com/AnaIitico/bitcoin_arbitrage](https://github.com/AnaIitico/bitcoin_arbitrage)

<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements

* [Img Shields](https://shields.io)
* [Choose an Open Source License](https://choosealicense.com)

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/AnaIitico/bitcoin_arbitrage.svg?style=for-the-badge
[contributors-url]: https://github.com/AnaIitico/bitcoin_arbitrage/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/AnaIitico/bitcoin_arbitrage.svg?style=for-the-badge
[forks-url]: https://github.com/AnaIitico/bitcoin_arbitrage/network/members
[stars-shield]: https://img.shields.io/github/stars/AnaIitico/bitcoin_arbitrage.svg?style=for-the-badge
[stars-url]: https://github.com/AnaIitico/bitcoin_arbitrage/stargazers
[issues-shield]: https://img.shields.io/github/issues/AnaIitico/bitcoin_arbitrage/network/members?style=for-the-badge
[issues-url]: https://github.com/AnaIitico/bitcoin_arbitrage/issues
<!-- [license-shield]: 
[license-url]:  -->
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/josetollinchi/
[exchange-january-screenshot]: /images/exchange_january_2018.JPG
[exchange-march-screenshot]: /images/exchange_march_2018.JPG
