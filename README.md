# pinescript_repo

//@version=5
indicator("EQL, EMA, & RSI Indicator", overlay=true)

// This script is a custom trading indicator for TradingView that combines the Exponential Moving Average (EMA) and the Relative Strength Index (RSI) to identify potential buy and sell signals. 
// It plots bullish and bearish reversal signals based on RSI levels and includes a 200-period EMA for trend analysis.

//====================================================================================================================
// Input parameters
length = input.int(14, title="Length")
src = input(close, title="Source")

// Calculate RSI
rsi = ta.rsi(src, length)

// Define overbought and oversold levels
overbought = 70
oversold = 30

// Identify reversal patterns
bullishReversal = ta.crossover(rsi, oversold)
bearishReversal = ta.crossunder(rsi, overbought)

// Plot signals on the chart
plotshape(series=bullishReversal, location=location.belowbar, color=color.green, style=shape.triangleup, text="BUY", textcolor=color.green)
plotshape(series=bearishReversal, location=location.abovebar, color=color.red, style=shape.triangledown, text="SELL", textcolor=color.red)

// Generate alerts
alertcondition(bullishReversal, title="Bullish Reversal", message="Bullish Reversal: Buy Signal")
alertcondition(bearishReversal, title="Bearish Reversal", message="Bearish Reversal: Sell Signal")

//====================================================================================================================

// Calculate and plot 200 EMA
ema200 = ta.ema(src, 200)
