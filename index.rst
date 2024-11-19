.. TrendVol documentation master file, created by
   sphinx-quickstart on Wed Nov 13 12:41:32 2024.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

TrendVol
========

|whop| |discord| |ninjatrader| |csharp| |dotnet|

Systematic Trading Strategy for NinjaTrader
===========================================
TrendVol is a fully-automated systematic trend-following strategy for NQ futures,
combining trend capture methods, volatility scaled position sizing and capital management techniques.
Position sizing is volatility adjusted, with risk scaled to maintain a user configurable 
annualized volatility target.

Key Features
============

* Trend detection algorithm using a single trend signal
* Breakout signals using N period lookback
* Dynamic volatility-based stop-losses
* Dual exit methods: Trailing stop loss or fixed risk/reward targets
* Volatility targetted position sizing
* User-defined risk capital allocation
* Built-in margin based position limits
* Three capital management methods: Fixed, Full Compounding, Half Compounding

System Requirements
===================

Platform
--------
* `NinjaTrader 8 <https://ninjatrader.com//>`_ platform
* Windows OS. Though, if you have Linux or Mac you can run on a `Windows VM <https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/>`_ or `Parallels <https://www.parallels.com/>`_
* Data feed subscription - Options:

   * `CME level 1 data <https://support.ninjatrader.com/s/article/How-do-I-register-for-data-feeds-for-my-account?language=en_US>`_ 
   * `Additional supported providers <https://ninjatrader.com/trading-platform/customize/market-data-brokerage-options/>`_.

Account Requirements
--------------------
* Recommended minimum account value: $2442 is the initial margin requirement for one Micro E-Mini NASDAQ 100 contract. See `margin requirements <https://ninjatrader.com/pricing/margins-position-management/>`_

Getting started
===============

Licensing
---------
TrendVol is available to license `here <https://whop.com/seceda/>`_.

License Activation
------------------
Upon purchase you will instantly receive a unique license key and a link to install the strategy.

#. Download strategy file
#. Input your provided license key

.. image:: /images/LicenseActivation.png

NinjaTrader Integration
-----------------------
#. From the Control Center window select the menu ``Tools > Import > NinjaScript Add-On``
#. Select ``C:\Seceda\TrendVol\Seceda_TrendVol_NT8.zip``

If you are having trouble importing the strategy view detailed guide `here <https://support.ninjatrader.com/s/article/How-Can-I-Import-Indicators-and-Strategies-into-NinjaTrader-Desktop?language=en_US#Step4>`_.

Apply strategy to chart
-----------------------
#. Apply strategy to NQ/MNQ ``30 minute`` chart. 
#. Set capital and risk parameters matching your account and risk appetite.

If you're having trouble applying the strategy to the chart view guide `here <https://ninjatrader.com/support/helpGuides/nt8/NT%20HelpGuide%20English.html?running_a_ninjascript_strategy.htm>`_.

Settings
========
* :ref:`Is_Backtest <Is_Backtest>`
* :ref:`Trend_Strength <Trend_Strength>`
* :ref:`Breakout_Period <Breakout_Period>`
* :ref:`Stop_Loss_Multiplier <Stop_Loss_Multiplier>`
* :ref:`Target_R <Target_R>`
* :ref:`Exit_Strategy <Exit_Strategy>`
* :ref:`Annual_Volatility_Target <Annual_Volatility_Target>`
* :ref:`Value_at_Risk <Value_at_Risk>`
* :ref:`Capital_Management <Capital_Management>`
* :ref:`Initial_Capital <Initial_Capital>`


.. |whop| image:: https://img.shields.io/badge/-Get%20access-FF6143?logo=data:image/svg%2bxml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz48c3ZnIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB2aWV3Qm94PSIwIDAgMzgzLjIgMTk2LjQiPjxnPjxwYXRoIGZpbGw9IndoaXRlIiBkPSJNNjAuOSwwQzM1LjcsMCwxOC40LDExLjEsNS4yLDIzLjVjMCwwLTUuMyw1LTUuMiw1LjJsNTUuMiw1NS4ybDU1LjItNTUuMkM5OS45LDE0LjMsODAuMiwwLDYwLjksMHoiLz48cGF0aCBmaWxsPSJ3aGl0ZSIgZD0iTTE5Ny4yLDBjLTI1LjIsMC00Mi41LDExLjEtNTUuNywyMy41YzAsMC00LjgsNC45LTUuMSw1LjJMNjguMiw5Ni45bDU1LjEsNTUuMUwyNDYuNiwyOC43QzIzNi4xLDE0LjMsMjE2LjUsMCwxOTcuMiwweiIvPjxwYXRoIGZpbGw9IndoaXRlIiBkPSJNMzMzLjgsMGMtMjUuMiwwLTQyLjUsMTEuMS01NS43LDIzLjVjMCwwLTUsNC45LTUuMiw1LjJMMTM2LjQsMTY1LjJsMTQuNCwxNC40YzIyLjMsMjIuMyw1OC45LDIyLjMsODEuMywwTDM4MywyOC43aDAuMkMzNzIuOCwxNC4zLDM1My4xLDAsMzMzLjgsMHoiLz48L2c+PC9zdmc+&logoColor=white
    :alt: Get access
    :target: https://whop.com/seceda/

.. |discord| image:: https://img.shields.io/discord/1115297620701761567?label=Discord&logo=discord&logoColor=white&color=5865F2
    :alt: Discord
    :target: https://discord.gg/p2uzRKKDdQ

.. |ninjatrader| image:: https://img.shields.io/badge/NinjaTrader-8-%23FF5500
    :alt: NinjaTrader 8
    :target: https://ninjatrader.com/

.. |csharp| image:: https://img.shields.io/badge/C%23-8.0-512BD4?logo=csharp&logoColor=white
    :alt: C# 8.0
    :target: https://docs.microsoft.com/en-us/dotnet/csharp/

.. |dotnet| image:: https://img.shields.io/badge/.NET-4.8-512BD4?logo=dotnet&logoColor=white
    :alt: .NET Framework 4.8
    :target: https://docs.microsoft.com/en-us/dotnet/

.. toctree::
   :maxdepth: 1
   :caption: Configuration
   :hidden:

   params/Parameters