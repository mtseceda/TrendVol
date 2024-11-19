Parameters
==========

.. py:class:: ExecutionMode

   .. py:property:: Is_Backtest(false)
   .. _Is_Backtest:

      :type: bool
      :default: False

      Controls whether the strategy runs in live or backtest mode.

      When ``False``:
         * Strategy operates in real-time trading mode
         * Uses actual account cash value for position sizing
      
      When ``True``:
         * Enables historical capital adjustment simulation
         * Properly simulates position sizing changes based on :py:attr:`Capital_Management` method
         * Required for accurate backtesting of ``HalfCompounding`` and ``FullCompounding`` methods

      .. note::
         Standard strategy backtesting does not dynamically adjust historical position sizes 
         as account value changes. Setting this to ``True`` enables proper simulation of 
         capital growth effects.


.. py:class:: Trend

   .. py:property:: Trend_Strength(10)
   .. _Trend_Strength:

      :type: int
      :default: 10
      :range: 1-20

      Controls trend detection sensitivity and signal quality using a single trend signal.

      * **Low values (1-5)**: More responsive, frequent signals
      * **Medium values (8-12)**: Balanced approach between signal frequency and trend detection.
      * **High values (15-20)**: Stricter trend filtering, fewer false signals

      .. note::
         Default of 10 provides optimal balance between trend capture and noise filtering.

   .. py:property:: Breakout_Period(5)
   .. _Breakout_Period:
      
      :type: int
      :default: 5
      :range: 1-100

      Sets the lookback period for entry price calculations.
      
      * Enters long positions using a Buy Stop Market order at the high of N periods

.. py:class:: RiskManagement

   .. py:property:: Stop_Loss_Multiplier(1.0)
   .. _Stop_Loss_Multiplier:

      :type: float
      :default: 1.0
      :range: 0.1-10.0

      Sets initial stop-loss distance as a multiple of daily volatility.

      * Higher values create wider stops, potentially reducing premature exits
      * Lower values offer tighter risk control but may increase likelihood of stopouts
      * Directly impacts average holding period of trades

   .. py:property:: Target_R(2.0)
   .. _Target_R:

      :type: float
      :default: 2.0
      :range: 0.1-10.0

      Sets profit target as a multiple of initial risk (R).
      
      * Only applies when :py:attr:`Exit_Strategy`` is ``TakeProfit``
      * Example: Value of 2.0 sets profit target at 2× the initial stop distance
      * Ignored when using trailing stops

   .. py:property:: Exit_Strategy(TrailingStopLoss)
   .. _Exit_Strategy:
      
      :type: enum
      :default: TrailingStopLoss
      :options: TrailingStopLoss, TakeProfit

      Defines the trade exit mechanism, critically impacting return distribution.

      ``TrailingStopLoss`` (Recommended):
        * Adaptive exit strategy that adjusts with market volatility
        * Preserves winning trades during sustained trends while maintaining defined risk
        * Best for capturing fat-tailed distributions in trend returns

      ``TakeProfit``:
        * Exits at fixed :py:attr:`Target_R`` multiple
        * Truncates return distribution by capping upside at predetermined level
        * Can improve win rate but often at expense of reduced expectancy
        * Increased trading friction through premature exits and reentries

.. py:class:: PositionSizing

   .. py:property:: Annual_Volatility_Target(0.25)
   .. _Annual_Volatility_Target:

      :type: float
      :default: 0.25
      :range: 0.01-1.0

      Defines the strategy's target annualized volatility, a key parameter in the position sizing algorithm that normalizes risk exposure across different market regimes.

      The position sizing formula uses:
        * target_vol is the Annual_Volatility_Target
        * 16 is the volatility scaling factor (√256 trading days)
        * daily_vol is the rolling N-day standard deviation

      Target Volatility Ranges:
        * **Conservative (5-15%)**: Market-neutral approach favoring stability over returns. Typical for low-risk portfolios and relative-value strategies.
        * **Moderate (15-25%)**: Standard for trend-following CTAs. Default 25% aligns with industry norms.
        * **Aggressive (25-100%)**: Higher return potential with proportional drawdown risk. Requires robust risk management and portfolio diversification.

   .. py:property:: Value_at_Risk(1.0)
   .. _Value_at_Risk:

      :type: float
      :default: 1.0
      :range: 0.01-1.0

      Defines the percentage of trading capital allocated to risk, functioning as a global risk exposure multiplier in the position sizing algorithm.

      .. note::
         :py:attr:`Value_at_Risk` acts as a overlay to :py:attr:`Annual_Volatility_Target`.
         While volatility targeting handles tactical sizing, VaR calculates positions as a proportion of the 'amount of capital you have at risk'

.. py:class:: CapitalManagement
   
   .. py:property:: Capital_Management(Fixed)
   .. _Capital_Management:

      :type: enum
      :default: Fixed
      :options: Fixed, FullCompounding, HalfCompounding

      Determines how position sizing adapts to account equity changes.

      ``Fixed``:
         * Maintains constant position sizes relative to initial capital
         * Ignores account equity changes
         * Suitable for consistent risk exposure

      ``FullCompounding``:
         * Scales position sizes with proportionally with total account equity
         * Maximizes geometric growth potential
         * Can lead to large positions after long profitable periods

      ``HalfCompounding``:
         * Reduces position sizes during drawdowns
         * Caps maximum size at initial capital level
         * Balances growth potential and capital preservation


   .. py:property:: Initial_Capital
   .. _Initial_Capital:

      :type: float

      Initial capital amount for used for position sizing calculations.

      * Set to actual starting account balance for live trading
      * Used as starting balance when :py:attr:`Is_Backtest` is ``True``