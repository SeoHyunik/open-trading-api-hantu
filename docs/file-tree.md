# Repository File Tree

`open-trading-api-hantu` — full ASCII treemap as of 2026-04-10.

Directories containing many similar leaf files use `(N items)` notation to keep the map readable.

```
open-trading-api-hantu/
├── .claude/
│   ├── CLAUDE.md
│   └── settings.local.json
├── MCP/
│   ├── KIS Code Assistant MCP/
│   │   ├── .dockerignore
│   │   ├── .gitignore
│   │   ├── .python-version
│   │   ├── Dockerfile
│   │   ├── README.md
│   │   ├── data.csv
│   │   ├── images/                          (10 .png screenshots)
│   │   ├── pyproject.toml
│   │   ├── server.py
│   │   ├── src/
│   │   │   ├── prompts/
│   │   │   │   └── prompt.py
│   │   │   └── utils/
│   │   │       └── api_searcher.py
│   │   └── uv.lock
│   ├── Kis Trading MCP/
│   │   ├── .dockerignore
│   │   ├── .env.live
│   │   ├── .gitignore
│   │   ├── .python-version
│   │   ├── Dockerfile
│   │   ├── Readme.md
│   │   ├── configs/
│   │   │   ├── auth.json
│   │   │   ├── domestic_bond.json
│   │   │   ├── domestic_futureoption.json
│   │   │   ├── domestic_stock.json
│   │   │   ├── elw.json
│   │   │   ├── etfetn.json
│   │   │   ├── overseas_futureoption.json
│   │   │   └── overseas_stock.json
│   │   ├── model/
│   │   │   ├── __init__.py
│   │   │   ├── auth.py
│   │   │   ├── base.py
│   │   │   ├── domestic_bond.py
│   │   │   ├── domestic_futureoption.py
│   │   │   ├── domestic_stock.py
│   │   │   ├── elw.py
│   │   │   ├── etfetn.py
│   │   │   ├── overseas_futureoption.py
│   │   │   ├── overseas_stock.py
│   │   │   └── updated.py
│   │   ├── module/
│   │   │   ├── __init__.py
│   │   │   ├── decorator.py
│   │   │   ├── factory.py
│   │   │   ├── middleware.py
│   │   │   └── plugin/
│   │   │       ├── __init__.py
│   │   │       ├── database.py
│   │   │       ├── environment.py
│   │   │       ├── kis.py
│   │   │       └── master_file.py
│   │   ├── pyproject.toml
│   │   ├── server.py
│   │   └── tools/
│   │       ├── __init__.py
│   │       ├── auth.py
│   │       ├── base.py
│   │       ├── domestic_bond.py
│   │       ├── domestic_futureoption.py
│   │       ├── domestic_stock.py
│   │       ├── elw.py
│   │       ├── etfetn.py
│   │       ├── overseas_futureoption.py
│   │       └── overseas_stock.py
│   ├── MCP AI 도구 연결 방법.md
│   └── README.MD
├── backtester/
│   ├── .env.example
│   ├── .gitignore
│   ├── README.md
│   ├── assets/                              (12 .png screenshots)
│   ├── backend/
│   │   ├── __init__.py
│   │   ├── main.py
│   │   ├── routes/
│   │   │   ├── __init__.py
│   │   │   ├── auth.py
│   │   │   ├── backtest.py
│   │   │   ├── files.py
│   │   │   ├── strategies.py
│   │   │   └── symbols.py
│   │   ├── schemas/
│   │   │   ├── __init__.py
│   │   │   ├── backtest.py
│   │   │   ├── file.py
│   │   │   └── strategy.py
│   │   └── state.py
│   ├── examples/
│   │   ├── README.md
│   │   ├── basic_backtest.py
│   │   ├── expert_strategies.py
│   │   ├── live_trading.py
│   │   ├── optimization.py
│   │   ├── output/
│   │   │   ├── .gitkeep
│   │   │   └── reports/
│   │   │       └── .gitkeep
│   │   ├── portfolio_analysis.py
│   │   ├── rule_builder.py
│   │   ├── strategy_generation.py
│   │   └── yaml_strategy.py
│   ├── frontend/
│   │   ├── .gitignore
│   │   ├── eslint.config.mjs
│   │   ├── next.config.ts
│   │   ├── package-lock.json
│   │   ├── package.json
│   │   ├── postcss.config.mjs
│   │   ├── src/
│   │   │   ├── app/
│   │   │   │   ├── backtest/
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── favicon.ico
│   │   │   │   ├── globals.css
│   │   │   │   ├── layout.tsx
│   │   │   │   └── page.tsx
│   │   │   ├── components/
│   │   │   │   ├── backtest/
│   │   │   │   │   ├── EquityChart.tsx
│   │   │   │   │   └── index.ts
│   │   │   │   ├── file/
│   │   │   │   │   ├── ExportButton.tsx
│   │   │   │   │   ├── FileDropZone.tsx
│   │   │   │   │   └── index.ts
│   │   │   │   ├── layout/
│   │   │   │   │   ├── Header.tsx
│   │   │   │   │   └── index.ts
│   │   │   │   ├── providers/
│   │   │   │   │   └── Providers.tsx
│   │   │   │   ├── settings/
│   │   │   │   │   ├── SettingsModal.tsx
│   │   │   │   │   └── index.ts
│   │   │   │   └── symbols/
│   │   │   │       ├── StockInput.tsx
│   │   │   │       └── index.ts
│   │   │   ├── contexts/
│   │   │   │   ├── AuthContext.tsx
│   │   │   │   └── index.ts
│   │   │   ├── hooks/
│   │   │   │   ├── index.ts
│   │   │   │   └── useAuth.ts
│   │   │   ├── lib/
│   │   │   │   ├── api/
│   │   │   │   │   ├── auth.ts
│   │   │   │   │   ├── backtest.ts
│   │   │   │   │   ├── client.ts
│   │   │   │   │   ├── files.ts
│   │   │   │   │   ├── index.ts
│   │   │   │   │   ├── strategies.ts
│   │   │   │   │   └── symbols.ts
│   │   │   │   └── utils.ts
│   │   │   └── types/
│   │   │       ├── auth.ts
│   │   │       ├── backtest.ts
│   │   │       ├── builder.ts
│   │   │       ├── file.ts
│   │   │       ├── index.ts
│   │   │       ├── strategy.ts
│   │   │       └── symbols.ts
│   │   └── tsconfig.json
│   ├── kis_auth.py
│   ├── kis_backtest/
│   │   ├── __init__.py
│   │   ├── client.py
│   │   ├── codegen/
│   │   │   ├── __init__.py
│   │   │   ├── generator.py
│   │   │   └── validator.py
│   │   ├── core/
│   │   │   ├── __init__.py
│   │   │   ├── candlestick.py
│   │   │   ├── condition.py
│   │   │   ├── converters.py
│   │   │   ├── indicator.py
│   │   │   ├── param_resolver.py
│   │   │   ├── risk.py
│   │   │   ├── schema.py
│   │   │   └── strategy.py
│   │   ├── dsl/
│   │   │   ├── __init__.py
│   │   │   ├── builder.py
│   │   │   └── helpers.py
│   │   ├── exceptions.py
│   │   ├── file/
│   │   │   ├── __init__.py
│   │   │   ├── loader.py
│   │   │   ├── python_exporter.py
│   │   │   ├── saver.py
│   │   │   ├── schema.py
│   │   │   └── templates/
│   │   │       ├── __init__.py
│   │   │       ├── consecutive_moves.kis.yaml
│   │   │       ├── false_breakout.kis.yaml
│   │   │       ├── ma_divergence.kis.yaml
│   │   │       ├── momentum.kis.yaml
│   │   │       ├── short_term_reversal.kis.yaml
│   │   │       ├── sma_crossover.kis.yaml
│   │   │       ├── strong_close.kis.yaml
│   │   │       ├── trend_filter_signal.kis.yaml
│   │   │       ├── volatility_breakout.kis.yaml
│   │   │       └── week52_high.kis.yaml
│   │   ├── lean/
│   │   │   ├── __init__.py
│   │   │   ├── data_converter.py
│   │   │   ├── executor.py
│   │   │   ├── optimizer.py
│   │   │   ├── project_manager.py
│   │   │   └── result_formatter.py
│   │   ├── models/
│   │   │   ├── __init__.py
│   │   │   ├── enums.py
│   │   │   ├── market_data.py
│   │   │   ├── result.py
│   │   │   └── trading.py
│   │   ├── portfolio/
│   │   │   ├── __init__.py
│   │   │   ├── analyzer.py
│   │   │   ├── rebalance.py
│   │   │   └── visualizer.py
│   │   ├── providers/
│   │   │   ├── __init__.py
│   │   │   ├── base.py
│   │   │   └── kis/
│   │   │       ├── __init__.py
│   │   │       ├── auth.py
│   │   │       ├── brokerage.py
│   │   │       ├── constants.py
│   │   │       ├── data.py
│   │   │       └── websocket.py
│   │   ├── report/
│   │   │   ├── __init__.py
│   │   │   ├── assets/
│   │   │   │   └── kis-report.css
│   │   │   ├── components/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── charts.py
│   │   │   │   ├── summary.py
│   │   │   │   └── tables.py
│   │   │   ├── generator.py
│   │   │   ├── portfolio_report.py
│   │   │   └── themes/
│   │   │       ├── __init__.py
│   │   │       ├── base.py
│   │   │       └── kis.py
│   │   ├── strategies/
│   │   │   ├── __init__.py
│   │   │   ├── base.py
│   │   │   ├── generator.py
│   │   │   ├── preset/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── consecutive_moves.py
│   │   │   │   ├── false_breakout.py
│   │   │   │   ├── ma_divergence.py
│   │   │   │   ├── momentum.py
│   │   │   │   ├── short_term_reversal.py
│   │   │   │   ├── sma_crossover.py
│   │   │   │   ├── strong_close.py
│   │   │   │   ├── trend_filter_signal.py
│   │   │   │   ├── volatility_breakout.py
│   │   │   │   └── week52_high.py
│   │   │   ├── registry.py
│   │   │   └── risk/
│   │   │       ├── __init__.py
│   │   │       └── position_sizer.py
│   │   └── utils/
│   │       ├── __init__.py
│   │       └── korean_market.py
│   ├── kis_mcp/
│   │   ├── __init__.py
│   │   ├── schemas.py
│   │   ├── server.py
│   │   └── tools/
│   │       ├── __init__.py
│   │       ├── backtest.py
│   │       ├── report.py
│   │       └── strategy.py
│   ├── pyproject.toml
│   ├── scripts/
│   │   ├── download_master.py
│   │   ├── setup_lean_data.sh
│   │   └── start_mcp.sh
│   └── start.sh
├── docs/
│   ├── convention.md
│   ├── file-tree.md                         ← this file
│   └── kospi-kosdaq-realtime-api.md
├── examples_llm/                            (API call examples, LLM-generated)
│   ├── kis_auth.py
│   ├── auth/
│   │   ├── auth_token/                      (auth_token.py, chk_auth_token.py)
│   │   └── auth_ws_token/                   (auth_ws_token.py, chk_auth_ws_token.py)
│   ├── domestic_bond/                       (18 subdirs, each with <name>.py + chk_<name>.py)
│   ├── domestic_futureoption/               (30 subdirs, each with <name>.py + chk_<name>.py)
│   ├── domestic_stock/                      (subdirs, each with <name>.py + chk_<name>.py)
│   ├── elw/                                 (subdirs, each with <name>.py + chk_<name>.py)
│   ├── etfetn/                              (subdirs, each with <name>.py + chk_<name>.py)
│   ├── overseas_futureoption/               (subdirs, each with <name>.py + chk_<name>.py)
│   └── overseas_stock/                      (subdirs, each with <name>.py + chk_<name>.py)
├── examples_user/                           (API call examples, user-authored; mirrors examples_llm structure)
│   ├── kis_auth.py
│   ├── auth/
│   ├── domestic_bond/
│   ├── domestic_futureoption/
│   ├── domestic_stock/
│   ├── elw/
│   ├── etfetn/
│   ├── overseas_futureoption/
│   └── overseas_stock/
├── legacy/
│   ├── README.md
│   ├── Sample01/
│   │   ├── README.md
│   │   ├── kis_api01.py
│   │   ├── kis_api02.py
│   │   ├── kis_api03.py
│   │   ├── kis_api04.py
│   │   ├── kis_auth.py
│   │   ├── kis_devlp.yaml
│   │   ├── kis_domfuopt.py
│   │   ├── kis_domstk.py
│   │   ├── kis_domstk_ws.py
│   │   ├── kis_ovrseafuopt.py
│   │   ├── kis_ovrseafuopt_ws.py
│   │   ├── kis_ovrseastk.py
│   │   └── kis_ovrseastk_ws.py
│   ├── Sample02/
│   │   ├── CSharp/
│   │   │   ├── Common.cs
│   │   │   ├── KIS_OverseaStk.cs
│   │   │   ├── Program.cs
│   │   │   └── kis_devlp_Sample.yaml
│   │   └── Make/
│   │       ├── POST 인풋예제1.PNG
│   │       └── POST 인풋예제2.PNG
│   ├── postman/
│   │   ├── README.md
│   │   ├── 모의계좌_POSTMAN_샘플코드_v1.6.json
│   │   ├── 모의계좌_POSTMAN_환경변수.json
│   │   ├── 실전계좌_POSTMAN_샘플코드_v2.6.json
│   │   └── 실전계좌_POSTMAN_환경변수.json
│   ├── rest/
│   │   ├── README.md
│   │   ├── config.yaml
│   │   ├── current_price_samle.py
│   │   ├── get_interest_stocks_price.py
│   │   ├── get_ovsfut_chart_price.py
│   │   ├── get_ovsstk_chart_price.py
│   │   ├── kis_api.py
│   │   ├── kis_auth.py
│   │   ├── kis_devlp.yaml
│   │   ├── kisdev_vi.yaml
│   │   ├── vba_sample.xlsm
│   │   └── 한국투자증권 오픈API엑셀_샘플(국내주식시세주문).xlsm
│   └── websocket/
│       ├── delphi/
│       │   ├── KISWebSocket.dpr
│       │   ├── KISWebSocket.dproj
│       │   ├── MainForm.dfm
│       │   └── MainForm.pas
│       └── python/
│           ├── multi_processing_sample_ws.py
│           ├── ops_ws_sample.py
│           ├── ws_commodity_future.py
│           ├── ws_domestic+overseas_stock.py
│           ├── ws_domestic_future.py
│           ├── ws_domestic_overseas_all.py
│           ├── ws_domestic_stock.py
│           ├── ws_overseas_future.py
│           └── ws_overseas_stock.py
├── stocks_info/
│   ├── domestic_bond_code.py
│   ├── domestic_cme_future_code.py
│   ├── domestic_commodity_future_code.py
│   ├── domestic_elw_code.py
│   ├── domestic_eurex_option_code.py
│   ├── domestic_index_future_code.py
│   ├── domestic_stock_future_code.py
│   ├── kis_konex_code_mst.py
│   ├── kis_kosdaq_code_mst.py
│   ├── kis_kospi_code_mst.py
│   ├── member_code.py
│   ├── overseas_future_code.py
│   ├── overseas_index_code.py
│   ├── overseas_stock_code.py
│   ├── sector_code.py
│   ├── theme_code.py
│   ├── 업종코드정보.h
│   ├── 종목마스터정보(ELW).h
│   ├── 종목마스터정보(상품선물옵션).h
│   ├── 종목마스터정보(주식선물옵션).h
│   ├── 종목마스터정보(지수선물옵션).h
│   ├── 종목마스터정보(채권).h
│   ├── 종목마스터정보(코넥스).h
│   ├── 종목마스터정보(코스닥).h
│   ├── 종목마스터정보(코스피).h
│   ├── 종목마스터정보(회원사).h
│   ├── 테마코드정보.h
│   ├── 해외선물정보.h
│   ├── 해외옵션정보.h
│   ├── 해외종목코드정보(미국,중국,일본,홍콩,베트남).h
│   ├── 해외주식옵션정보.h
│   └── 해외주식지수정보.h
├── strategy_builder/
│   ├── README.md
│   ├── assets/                              (10 .png screenshots)
│   ├── backend/
│   │   ├── __init__.py
│   │   ├── main.py
│   │   ├── routers/
│   │   │   ├── __init__.py
│   │   │   ├── account.py
│   │   │   ├── auth.py
│   │   │   ├── files.py
│   │   │   ├── market.py
│   │   │   ├── orders.py
│   │   │   ├── strategy.py
│   │   │   └── symbols.py
│   │   └── state.py
│   ├── core/
│   │   ├── __init__.py
│   │   ├── candlestick.py
│   │   ├── data_fetcher.py
│   │   ├── indicators.py
│   │   ├── order_executor.py
│   │   ├── position_manager.py
│   │   ├── risk_manager.py
│   │   ├── signal.py
│   │   └── websocket_manager.py
│   ├── examples/
│   │   ├── README.md
│   │   └── run_all_strategies.py
│   ├── frontend/
│   │   ├── .env.example
│   │   ├── .gitignore
│   │   ├── eslint.config.mjs
│   │   ├── next.config.ts
│   │   ├── package-lock.json
│   │   ├── package.json
│   │   ├── postcss.config.mjs
│   │   ├── src/                             (app/, components/, contexts/, hooks/, lib/, types/)
│   │   └── tsconfig.json
│   ├── kis_auth.py
│   ├── pyproject.toml
│   ├── start.sh
│   ├── strategy/
│   │   ├── __init__.py
│   │   ├── base_strategy.py
│   │   ├── strategy_01_golden_cross.py
│   │   ├── strategy_02_momentum.py
│   │   ├── strategy_03_week52_high.py
│   │   ├── strategy_04_consecutive.py
│   │   ├── strategy_05_disparity.py
│   │   ├── strategy_06_breakout_fail.py
│   │   ├── strategy_07_strong_close.py
│   │   ├── strategy_08_volatility.py
│   │   ├── strategy_09_mean_reversion.py
│   │   └── strategy_10_trend_filter.py
│   └── strategy_core/
│       ├── __init__.py
│       ├── dsl/
│       │   ├── __init__.py
│       │   ├── codegen.py
│       │   ├── converter.py
│       │   └── parser.py
│       ├── executor.py
│       ├── name_utils.py
│       ├── preset/
│       │   ├── __init__.py
│       │   ├── breakout_fail.py
│       │   ├── consecutive.py
│       │   ├── disparity.py
│       │   ├── golden_cross.py
│       │   ├── mean_reversion.py
│       │   ├── momentum.py
│       │   ├── strong_close.py
│       │   ├── trend_filter.py
│       │   ├── volatility.py
│       │   └── week52_high.py
│       └── registry.py
├── tools/
│   └── run-cycle.ps1
├── .gitignore
├── README.md
├── kis_devlp.yaml
├── pyproject.toml
├── requirements.txt
└── uv.lock
```

---

> Total tracked files: ~1,646 (excluding `.git/` and `.idea/`).
> Large uniform subtrees (`examples_llm`, `examples_user`) are collapsed to their subdirectory names; each leaf dir contains `<endpoint>.py` + `chk_<endpoint>.py`.
