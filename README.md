# Financial Market Dashboard — version dated 17 September 2026

This is a separate version of the dashboard. The existing published site is unchanged. The report date shown on the page updates each day when data reloads.

## Open locally

On Windows, double-click `start-dashboard.cmd`. It starts the local data service and opens <http://127.0.0.1:8767/>. Keep the computer running while viewing this local address.

The EODHD token is read from the existing private `work/.eodhd-token` file two folders above this directory, or from the `EODHD_API_TOKEN` environment variable. Never add a token to the HTML or a GitHub repository.

## Publish separately on Render

To publish this version, put this directory's files in a **new** GitHub repository and create a new Render service from its `render.yaml`. Set the secret `EODHD_API_TOKEN` in Render. This version has a distinct Render service name (`new-macro-dashboard-v2`) so it will not replace the existing site.

The Blueprint selects Render's Free web service plan. Render puts idle Free services to sleep and displays its own startup page to the next visitor. The dashboard's loading placeholders appear only after the server has started. A paid web service plan removes idle spin-down; alternatively, a separately hosted static frontend could present a branded waiting screen while this backend wakes up.

## Data notes

The dashboard uses MOEX data for RENI, Bank of Russia for USD/RUB, EUR/RUB and the key rate, Bank of Canada for CAD/USD, and EODHD for CURA.TO. Federal Reserve target range is loaded from FRED and checked against the most recent official FOMC statement, which can publish before the FRED daily observation. Curaleaf shares use reported data from EODHD when available, with a dated SEC filing fallback. Missing data shows an error instead of an invented value.

Each KPI card has a History control showing the previous 10 calendar days, except RENI 20D ADTV, which shows 30 actual trading sessions in one table. Price, FX, policy rate and market capitalization histories use compact charts. The RENI 20D ADTV history recalculates the cash average for each session using that date's latest 20 trading sessions, with weekends and days without trades excluded. Its 7d Forecast uses the average daily cash turnover of the last seven actual MOEX sessions for each of the next seven assumed trading weekdays. Future exchange holidays are not known to the forecast, so the forecast dates are provisional. Projected values are labeled as a scenario rather than market data.

The ADTV history table keeps a light background and shows a blue bar next to each numeric value. Bar lengths compare values within their own column. The forecast table shows numbers without bars; forecast rows below ₽60 million are pink and below ₽50 million red. When any of the seven forecast values is below ₽60 million, a centered covenant-risk alert appears after the data loads. It can be closed with ×, or its “See 7 days forecast” button opens the forecast table. The header contains the dashboard date, last data check time and a green refresh button in one row on a wide screen.
