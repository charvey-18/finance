# Three-Statement Interview Diagrams

These diagrams use one sign convention throughout:

- Operating asset up = use of cash
- Operating asset down = source of cash
- Operating liability up = source of cash
- Operating liability down = use of cash

Color key used below:

- Blue = income statement
- Green = cash flow statement
- Amber = balance sheet
- Red = use of cash
- Mint = source of cash
- Gray = note or bridge item

## Vertical Three-Statement Reference

This is the big-picture view. Each statement is stacked vertically so you can see how net income rolls into cash flow and how ending cash and retained earnings land on the balance sheet.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '24px'}, 'flowchart': {'htmlLabels': true, 'nodeSpacing': 60, 'rankSpacing': 90, 'useMaxWidth': true}} }%%
flowchart TD
  subgraph O_IS["Income Statement"]
    direction TB
    O_REV["Revenue"]
    O_COGS["Less COGS"]
    O_GP["Gross profit"]
    O_OPEX["Less OpEx"]
    O_EBITDA["EBITDA"]
    O_DA["Less D&A"]
    O_EBIT["EBIT"]
    O_INT["Less interest"]
    O_EBT["EBT"]
    O_TAX["Less taxes"]
    O_NI["Net income"]
    O_REV --> O_COGS --> O_GP --> O_OPEX --> O_EBITDA --> O_DA --> O_EBIT --> O_INT --> O_EBT --> O_TAX --> O_NI
  end

  subgraph O_CFS["Cash Flow Statement"]
    direction TB
    O_NI2["Net income"]
    O_NON["Add back D&A and other non-cash"]
    O_WC["Adjust delta NWC"]
    O_CFO["CFO"]
    O_CAPEX["CapEx"]
    O_CFI["CFI"]
    O_FIN["Debt and equity flows"]
    O_CFF["CFF"]
    O_NC["Net change in cash"]
    O_NI2 --> O_NON --> O_WC --> O_CFO --> O_CAPEX --> O_CFI --> O_FIN --> O_CFF --> O_NC
  end

  subgraph O_BS["Balance Sheet"]
    direction TB
    O_CASH["Cash"]
    O_OA["Operating assets"]
    O_PPE["PP&E"]
    O_OL["Operating liabilities"]
    O_DEBT["Debt"]
    O_RE["Retained earnings"]
    O_CASH --> O_OA --> O_PPE --> O_OL --> O_DEBT --> O_RE
  end

  O_NI -->|start CFS with NI| O_NI2
  O_NC -->|net change updates cash| O_CASH
  O_NI -.->|NI closes to RE| O_RE

  classDef is fill:#dbeafe,stroke:#1d4ed8,color:#0f172a,stroke-width:1.5px;
  classDef cfs fill:#dcfce7,stroke:#15803d,color:#14532d,stroke-width:1.5px;
  classDef bs fill:#fef3c7,stroke:#b45309,color:#78350f,stroke-width:1.5px;
  classDef note fill:#f8fafc,stroke:#64748b,color:#334155,stroke-width:1.5px;

  class O_REV,O_COGS,O_GP,O_OPEX,O_EBITDA,O_DA,O_EBIT,O_INT,O_EBT,O_TAX,O_NI is;
  class O_NI2,O_NON,O_WC,O_CFO,O_CAPEX,O_CFI,O_FIN,O_CFF,O_NC cfs;
  class O_CASH,O_OA,O_PPE,O_OL,O_DEBT,O_RE bs;

  style O_IS fill:#eff6ff,stroke:#1d4ed8,stroke-width:2px,color:#0f172a
  style O_CFS fill:#f0fdf4,stroke:#15803d,stroke-width:2px,color:#14532d
  style O_BS fill:#fff7ed,stroke:#b45309,stroke-width:2px,color:#78350f
```

## Scope Notes: What usually counts as CapEx and NWC?

`CapEx` and `delta NWC` are where interview answers often get sloppy. In a clean interview answer, define them explicitly: `CapEx` is capitalized operating investment in long-lived assets, and `operating NWC` is operating current assets minus operating current liabilities. Company definitions can vary, so it is good practice to state your scope before walking through the bridge.

Quick definitions:

- `Accounts receivable (AR)`: money customers owe the company because revenue was booked before cash was collected. It is an operating asset.
- `Accounts payable (AP)`: money the company owes suppliers or vendors because inventory or expense was booked before cash was paid. It is an operating liability.
- `Prepaids`: cash the company paid upfront for a future expense. It is an operating asset until the expense is recognized.
- `Accrued expenses`: expenses already recognized on the income statement but not yet paid in cash. They are operating liabilities.
- `Deferred revenue`: cash collected before the company recognizes the revenue. It is an operating liability until the revenue is earned.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '22px'}, 'flowchart': {'htmlLabels': true, 'nodeSpacing': 55, 'rankSpacing': 85, 'useMaxWidth': true}} }%%
flowchart TD
  subgraph S_NWC["Operating NWC scope"]
    S_NWC0["Operating NWC = operating current assets - operating current liabilities"]
    S_NWC0 --> S_NWCA["Usually include asset side"]
    S_NWC0 --> S_NWCL["Usually include liability side"]
    S_NWC0 --> S_NWCX["Usually exclude"]

    S_NWCA --> S_AR["Accounts receivable"]
    S_NWCA --> S_INV["Inventory"]
    S_NWCA --> S_PRE["Prepaids"]

    S_NWCL --> S_AP["Accounts payable"]
    S_NWCL --> S_ACC["Accrued expenses"]
    S_NWCL --> S_DEF["Deferred revenue"]

    S_NWCX --> S_CASH["Cash and marketable securities"]
    S_NWCX --> S_DEBT["Debt and current maturities"]
    S_NWCX --> S_TAX["Taxes and interest payable"]
    S_NWCX --> S_NONOP["One-time or non-operating items"]
  end

  subgraph S_CAP["CapEx scope"]
    S_CAP0["CapEx = capitalized operating investment"]
    S_CAP0 --> S_CAPI["Usually include"]
    S_CAP0 --> S_CAPX["Usually not included"]

    S_CAPI --> S_PPE["PP&E purchases"]
    S_CAPI --> S_BUILD["Leasehold improvements and build-outs"]
    S_CAPI --> S_EQUIP["Equipment, vehicles, servers"]
    S_CAPI --> S_SOFT["Capitalized software"]
    S_CAPI --> S_MG["Maintenance and growth CapEx"]

    S_CAPX --> S_REPAIR["Routine repairs in OpEx"]
    S_CAPX --> S_MA["M&A or business acquisitions"]
    S_CAPX --> S_FIN["Debt principal or other financing uses"]
  end

  classDef is fill:#dbeafe,stroke:#1d4ed8,color:#0f172a,stroke-width:1.5px;
  classDef cfs fill:#dcfce7,stroke:#15803d,color:#14532d,stroke-width:1.5px;
  classDef bs fill:#fef3c7,stroke:#b45309,color:#78350f,stroke-width:1.5px;
  classDef use fill:#fee2e2,stroke:#dc2626,color:#7f1d1d,stroke-width:1.5px;
  classDef note fill:#f8fafc,stroke:#64748b,color:#334155,stroke-width:1.5px;

  class S_NWC0,S_CAP0 note;
  class S_NWCA,S_NWCL,S_CAPI cfs;
  class S_AR,S_INV,S_PRE,S_AP,S_ACC,S_DEF,S_PPE,S_BUILD,S_EQUIP,S_SOFT,S_MG bs;
  class S_NWCX,S_CAPX,S_CASH,S_DEBT,S_TAX,S_NONOP,S_REPAIR,S_MA,S_FIN use;

  style S_NWC fill:#fff7ed,stroke:#b45309,stroke-width:2px,color:#78350f
  style S_CAP fill:#f0fdf4,stroke:#15803d,stroke-width:2px,color:#14532d
```

Interview script:

- In interview shorthand, operating NWC usually means `AR + inventory + prepaids - AP - accrued expenses - deferred revenue`.
- I usually exclude cash, debt, marketable securities, and other non-operating items unless the case tells me otherwise.
- CapEx is capitalized spend on long-lived operating assets, not just any cash outflow.
- Typical CapEx includes PP&E, store or facility build-outs, equipment, and sometimes capitalized software.
- Routine repairs and maintenance usually stay in operating expenses, so they are not CapEx.
- In valuation, I may separate maintenance CapEx from growth CapEx if the question is about steady-state cash flow.
- If the company uses a different definition, I say the exact scope before walking through the cash flow bridge.

## A. How do you get from EBITDA to levered free cash flow?

EBITDA is an earnings proxy, not cash flow. To get to levered free cash flow, you move from operating profit before non-cash charges to actual cash left after taxes, interest, CapEx, working capital needs, and, if relevant, required debt paydown. For interview purposes, `CapEx` usually means capitalized operating investment, and `delta NWC` usually means the change in operating current assets and operating current liabilities, not every balance sheet current item.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '22px'}, 'flowchart': {'htmlLabels': true, 'nodeSpacing': 50, 'rankSpacing': 80, 'useMaxWidth': true}} }%%
flowchart TD
  subgraph A1["Bridge 1: EBITDA route"]
    A_EBITDA["EBITDA (IS)"] -->|less cash taxes| A_TAX["After-tax operating cash"]
    A_TAX -->|less cash interest| A_INT["After-interest cash"]
    A_INT -->|less CapEx| A_CAP["After CapEx"]
    A_CAP -->|minus NWC up plus NWC down| A_WC["After NWC"]
    A_WC -->|less mandatory debt amort.| A_LFCF["Levered FCF"]
  end

  subgraph A2["Bridge 2: Equivalent NI route"]
    A_NI["Net income (IS)"] -->|add D&A| A_DA["Add back D&A"]
    A_DA -->|+/- other non-cash items| A_NON["Cash earnings before WC"]
    A_NON -->|minus NWC up plus NWC down| A_CFO["CFO"]
    A_CFO -->|less CapEx| A_POSTCAP["Cash after CapEx"]
    A_POSTCAP -->|less mandatory debt amort.| A_LFCF
  end

  A_CT["Cash taxes (CFS; taxes payable on BS)"] -.->|subtract| A_TAX
  A_CI["Cash interest (CFS; debt on BS)"] -.->|subtract| A_INT
  A_CX["CapEx (CFI; PP&E on BS)"] -.->|subtract| A_CAP
  A_NWCNOTE["Delta NWC (BS into CFO) Asset up = use Liability up = source"] -.->|adjust| A_WC
  A_DEBT["Mandatory amort. (CFF; debt down on BS)"] -.->|subtract| A_LFCF
  A_CAPWHAT["CapEx usually = PP&E, build-outs, equipment, capitalized software"] -.-> A_CX
  A_NWCWHAT["Operating NWC usually = AR + inventory + prepaids - AP - accrued - deferred rev"] -.-> A_NWCNOTE
  A_NWCEX["Usually exclude cash, debt, taxes, and one-time items"] -.-> A_NWCNOTE

  classDef is fill:#dbeafe,stroke:#1d4ed8,color:#0f172a,stroke-width:1.5px;
  classDef cfs fill:#dcfce7,stroke:#15803d,color:#14532d,stroke-width:1.5px;
  classDef note fill:#f8fafc,stroke:#64748b,color:#334155,stroke-width:1.5px;
  classDef result fill:#ccfbf1,stroke:#0f766e,color:#134e4a,stroke-width:2px;

  class A_EBITDA,A_NI is;
  class A_TAX,A_INT,A_CAP,A_CFO,A_POSTCAP,A_CT,A_CI,A_CX,A_DEBT cfs;
  class A_DA,A_NON,A_NWCNOTE,A_CAPWHAT,A_NWCWHAT,A_NWCEX note;
  class A_WC,A_LFCF result;
```

Interview script:

- Start with EBITDA, which is before interest, taxes, and non-cash D&A.
- Subtract cash taxes and cash interest, because levered free cash flow is after both.
- Here, CapEx usually means capitalized operating spend like equipment, facilities, build-outs, and capitalized software.
- Subtract CapEx, because that is a real cash outflow even though it is not an immediate income statement expense.
- Then adjust for changes in net working capital: operating NWC usually means AR, inventory, prepaids, AP, accrued expenses, and deferred revenue.
- NWC up is a use of cash, NWC down is a source of cash, but I usually exclude cash, debt, taxes, and one-time items unless told otherwise.
- If the company has required debt amortization, subtract that too to get the cash left for equity.
- The equivalent bridge is net income plus D&A and other non-cash items, minus CapEx, minus or plus delta NWC, and minus required principal paydown.
- A common interview trap is calling EBITDA cash flow; it is only the starting point.

## B. How do you get from net income to cash from operations?

Under the indirect method, cash from operations starts with net income, then reverses non-cash items and timing differences. The goal is to turn accounting profit into cash generated by the core business in the period. The working capital adjustment here is usually `operating` working capital, not cash, debt, or financing items.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '22px'}, 'flowchart': {'htmlLabels': true, 'nodeSpacing': 50, 'rankSpacing': 80, 'useMaxWidth': true}} }%%
flowchart TD
  subgraph B1["Income Statement"]
    B_NI["Net income (IS)"]
  end

  subgraph B2["Non-cash and non-op adjustments"]
    B_DA["D&A"]
    B_ONC["Other non-cash items"]
    B_GLS["Remove non-op gains / losses"]
  end

  subgraph B3["Working capital from BS"]
    B_ASSET["AR / inventory / prepaids"]
    B_LIAB["AP / accrued / deferred rev"]
  end

  B_NI -->|start here| B_PRE["Cash earnings before WC"]
  B_DA -->|add back| B_PRE
  B_ONC -->|add back| B_PRE
  B_GLS -->|reverse if needed| B_PRE
  B_PRE -->|adjust delta working capital| B_CFO["CFO (CFS)"]

  B_ASSET -.->|up = use of cash down = source of cash| B_CFO
  B_LIAB -.->|up = source of cash down = use of cash| B_CFO

  classDef is fill:#dbeafe,stroke:#1d4ed8,color:#0f172a,stroke-width:1.5px;
  classDef cfs fill:#dcfce7,stroke:#15803d,color:#14532d,stroke-width:1.5px;
  classDef bs fill:#fef3c7,stroke:#b45309,color:#78350f,stroke-width:1.5px;
  classDef note fill:#f8fafc,stroke:#64748b,color:#334155,stroke-width:1.5px;

  class B_NI is;
  class B_CFO cfs;
  class B_ASSET,B_LIAB bs;
  class B_DA,B_ONC,B_GLS,B_PRE note;
```

Interview script:

- Start with net income because the cash flow statement reconciles accounting earnings to cash.
- Add back non-cash expenses like depreciation, amortization, and other non-cash charges.
- Reverse non-operating gains or losses if they affected net income but belong somewhere else in cash flow.
- Then adjust for working capital timing items from the balance sheet, usually AR, inventory, prepaids, AP, accrued expenses, and deferred revenue.
- If operating assets go up, cash goes down; if they go down, cash goes up.
- If operating liabilities go up, cash goes up; if they go down, cash goes down.
- I usually do not include cash, debt, or other financing items in that operating NWC adjustment.
- The result is cash from operations, which is cash generated by the core business before investing and financing flows.

## C. How do changes in working capital flow through the 3 statements?

Working capital changes are timing differences between the income statement and actual cash movement. The balance sheet captures the asset or liability build, and the cash flow statement converts that change into a source or use of cash. In most interview settings, operating NWC means `AR + inventory + prepaids - AP - accrued expenses - deferred revenue`, while cash, debt, and most tax items are treated separately. `AR` means receivables from customers; `AP` means payables owed to suppliers. `Prepaids` are cash paid before expense recognition, `accrued expenses` are expenses recognized before cash payment, and `deferred revenue` is cash received before revenue recognition.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '22px'}, 'flowchart': {'htmlLabels': true, 'nodeSpacing': 50, 'rankSpacing': 80, 'useMaxWidth': true}} }%%
flowchart TD
  subgraph C_ASSETS["Operating assets: increase = use, decrease = source"]
    subgraph C_AR["AR (BS asset; tied to revenue on IS)"]
      C_AR1["Revenue booked, cash later"] --> C_ARU["AR up"] -->|Use of cash| C_ARC1["CFO down (CFS)"]
      C_AR2["Receivables collected"] --> C_ARD["AR down"] -->|Source of cash| C_ARC2["CFO up (CFS)"]
    end

    subgraph C_INV["Inventory (BS asset; tied to COGS on IS)"]
      C_INV1["Buy or build more than sold"] --> C_INVU["Inventory up"] -->|Use of cash| C_INVC1["CFO down (CFS)"]
      C_INV2["Sell existing stock or buy less"] --> C_INVD["Inventory down"] -->|Source of cash| C_INVC2["CFO up (CFS)"]
    end

    subgraph C_PRE["Prepaids (BS asset; tied to opex on IS)"]
      C_PRE1["Cash paid before expense"] --> C_PREU["Prepaids up"] -->|Use of cash| C_PREC1["CFO down (CFS)"]
      C_PRE2["Expense recognized, no new cash"] --> C_PRED["Prepaids down"] -->|Source of cash| C_PREC2["CFO up (CFS)"]
    end
  end

  subgraph C_LIAB["Operating liabilities: increase = source, decrease = use"]
    subgraph C_AP["AP (BS liability; tied to inventory or opex)"]
      C_AP1["Expense booked, supplier unpaid"] --> C_APU["AP up"] -->|Source of cash| C_APC1["CFO up (CFS)"]
      C_AP2["Supplier paid"] --> C_APD["AP down"] -->|Use of cash| C_APC2["CFO down (CFS)"]
    end

    subgraph C_ACC["Accrued expenses (BS liability; tied to opex on IS)"]
      C_ACC1["Expense booked, cash unpaid"] --> C_ACCU["Accrued exp up"] -->|Source of cash| C_ACCC1["CFO up (CFS)"]
      C_ACC2["Accrual paid"] --> C_ACCD["Accrued exp down"] -->|Use of cash| C_ACCC2["CFO down (CFS)"]
    end

    subgraph C_DEF["Deferred revenue (BS liability; tied to revenue on IS)"]
      C_DEF1["Cash received before revenue"] --> C_DEFU["Deferred rev up"] -->|Source of cash| C_DEFC1["CFO up (CFS)"]
      C_DEF2["Revenue recognized from prior cash"] --> C_DEFD["Deferred rev down"] -->|Use of cash| C_DEFC2["CFO down (CFS)"]
    end
  end

  classDef bs fill:#fef3c7,stroke:#b45309,color:#78350f,stroke-width:1.5px;
  classDef use fill:#fee2e2,stroke:#dc2626,color:#7f1d1d,stroke-width:1.5px;
  classDef source fill:#dcfce7,stroke:#16a34a,color:#14532d,stroke-width:1.5px;
  classDef note fill:#f8fafc,stroke:#64748b,color:#334155,stroke-width:1.5px;

  class C_ARU,C_INVU,C_PREU,C_APD,C_ACCD,C_DEFD,C_ARC1,C_INVC1,C_PREC1,C_APC2,C_ACCC2,C_DEFC2 use;
  class C_ARD,C_INVD,C_PRED,C_APU,C_ACCU,C_DEFU,C_ARC2,C_INVC2,C_PREC2,C_APC1,C_ACCC1,C_DEFC1 source;
  class C_AR1,C_AR2,C_INV1,C_INV2,C_PRE1,C_PRE2,C_AP1,C_AP2,C_ACC1,C_ACC2,C_DEF1,C_DEF2 note;

  style C_ASSETS fill:#fff7ed,stroke:#ea580c,stroke-width:2px,color:#431407
  style C_LIAB fill:#f0fdf4,stroke:#16a34a,stroke-width:2px,color:#14532d
  style C_AR fill:#fffbeb,stroke:#b45309,stroke-width:1.5px,color:#78350f
  style C_INV fill:#fffbeb,stroke:#b45309,stroke-width:1.5px,color:#78350f
  style C_PRE fill:#fffbeb,stroke:#b45309,stroke-width:1.5px,color:#78350f
  style C_AP fill:#fffbeb,stroke:#b45309,stroke-width:1.5px,color:#78350f
  style C_ACC fill:#fffbeb,stroke:#b45309,stroke-width:1.5px,color:#78350f
  style C_DEF fill:#fffbeb,stroke:#b45309,stroke-width:1.5px,color:#78350f
```

Interview script:

- Working capital is mostly about timing between the income statement and cash.
- AR is money customers owe you after you book revenue; it is an operating asset.
- AP is money you owe suppliers after you book inventory or expense; it is an operating liability.
- In interviews, I usually define operating NWC as AR, inventory, and prepaids minus AP, accrued expenses, and deferred revenue.
- For AR, up means you booked revenue but did not collect cash yet, so cash is down; down means collection, so cash is up.
- For inventory and prepaids, up means cash went out before the expense fully hit earnings, so that is a use of cash.
- For AP and accrued expenses, up means you recognized expense but have not paid cash yet, so that is a source of cash.
- For deferred revenue, up means you got cash before recognizing revenue, so cash is up even though revenue is still deferred.
- I usually exclude cash, debt, interest payable, and taxes payable from this operating NWC bucket unless the question defines it differently.
- The core sign rule is simple: operating asset up equals use, operating liability up equals source.
- A common trap is flipping the sign on AR or inventory; both are assets, so an increase consumes cash.

## D. How does depreciation affect the 3 statements?

Depreciation lowers accounting earnings but does not use cash in the current period. The key interview point is that it reduces EBIT and net income on the income statement, gets added back on the cash flow statement, and reduces net PP&E on the balance sheet.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '22px'}, 'flowchart': {'htmlLabels': true, 'nodeSpacing': 50, 'rankSpacing': 80, 'useMaxWidth': true}} }%%
flowchart LR
  subgraph D_IS["Income Statement"]
    D_DEP["Depreciation expense"] -->|non-cash expense| D_EBIT["EBIT down"]
    D_EBIT --> D_TAX["Taxes down"]
    D_TAX --> D_NI["Net income down"]
  end

  subgraph D_CFS["Cash Flow Statement"]
    D_NI --> D_CFO1["CFO starts lower via NI"]
    D_DEP -->|add back: no cash left today| D_ADD["Add back depreciation"]
    D_CFO1 --> D_CFO2["CFO after add-back"]
    D_ADD --> D_CFO2
    D_TAX -->|lower cash taxes| D_SHIELD["Tax shield"]
    D_SHIELD --> D_CFO2
  end

  subgraph D_BS["Balance Sheet"]
    D_PPE["Net PP&E down"]
    D_CASH["Cash up by tax shield"]
    D_RE["Retained earnings down after tax"]
  end

  D_DEP -->|contra asset effect| D_PPE
  D_CFO2 --> D_CASH
  D_NI --> D_RE

  classDef is fill:#dbeafe,stroke:#1d4ed8,color:#0f172a,stroke-width:1.5px;
  classDef cfs fill:#dcfce7,stroke:#15803d,color:#14532d,stroke-width:1.5px;
  classDef bs fill:#fef3c7,stroke:#b45309,color:#78350f,stroke-width:1.5px;

  class D_DEP,D_EBIT,D_TAX,D_NI is;
  class D_CFO1,D_ADD,D_CFO2,D_SHIELD cfs;
  class D_PPE,D_CASH,D_RE bs;
```

Interview script:

- Depreciation is an expense on the income statement, so EBIT and net income go down.
- It is non-cash, so you add it back in cash from operations.
- That means depreciation does not reduce cash by itself in the current period.
- The real cash effect is the tax shield, because lower pretax income means lower cash taxes.
- On the balance sheet, net PP&E goes down because accumulated depreciation rises.
- Retained earnings also go down because net income is lower.
- The classic interview trap is saying depreciation is a cash expense; it is not.

## E. How does CapEx affect the 3 statements?

CapEx is a real cash outflow, but it is capitalized on the balance sheet rather than expensed immediately on the income statement. The income statement effect comes later through depreciation or amortization. In practice, CapEx often includes PP&E purchases, equipment, leasehold improvements, facilities build-outs, and sometimes capitalized software. It usually does not include routine repairs, which stay in operating expenses.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '22px'}, 'flowchart': {'htmlLabels': true, 'nodeSpacing': 50, 'rankSpacing': 80, 'useMaxWidth': true}} }%%
flowchart LR
  subgraph E_CFS["Cash Flow Statement"]
    E_CAP["CapEx spend"] -->|use of cash in CFI| E_CASHNOW["Cash down now"]
    E_DEP2["Later depreciation"] -->|added back in CFO| E_CFOADD["CFO add-back later"]
  end

  subgraph E_BS["Balance Sheet"]
    E_PPE["Gross PP&E up now"]
    E_CASHBS["Cash down"]
    E_NPPE["Net PP&E down later via depreciation"]
    E_RE["Retained earnings down later"]
  end

  subgraph E_IS["Income Statement"]
    E_NOIS["No immediate P&L hit"]
    E_DEP["Future depreciation"]
    E_EARN["EBIT and NI down later"]
  end

  E_CAP -->|capitalized, not expensed now| E_PPE
  E_CAP --> E_NOIS
  E_CASHNOW --> E_CASHBS
  E_PPE -->|over useful life| E_DEP
  E_DEP --> E_EARN
  E_DEP --> E_DEP2
  E_DEP --> E_NPPE
  E_EARN --> E_RE
  E_CAPIN["Includes PP&E, equipment, build-outs, capitalized software"] -.-> E_CAP
  E_CAPOUT["Repairs stay in OpEx; M&A is separate"] -.-> E_NOIS

  classDef is fill:#dbeafe,stroke:#1d4ed8,color:#0f172a,stroke-width:1.5px;
  classDef cfs fill:#dcfce7,stroke:#15803d,color:#14532d,stroke-width:1.5px;
  classDef bs fill:#fef3c7,stroke:#b45309,color:#78350f,stroke-width:1.5px;
  classDef note fill:#f8fafc,stroke:#64748b,color:#334155,stroke-width:1.5px;

  class E_DEP,E_EARN is;
  class E_CAP,E_CASHNOW,E_DEP2,E_CFOADD cfs;
  class E_PPE,E_CASHBS,E_NPPE,E_RE bs;
  class E_NOIS,E_CAPIN,E_CAPOUT note;
```

Interview script:

- CapEx is cash going out today, so it shows up as a use of cash in investing cash flow.
- CapEx usually includes long-lived operating investment like PP&E, equipment, build-outs, and sometimes capitalized software.
- It does not hit the income statement right away because you capitalize it on the balance sheet.
- Immediately, cash goes down and PP&E goes up.
- Over time, the asset is depreciated, and that depreciation reduces EBIT and net income.
- That later depreciation is non-cash, so it gets added back in CFO.
- Routine repairs usually stay in opex, and I may separate maintenance CapEx from growth CapEx in valuation work.
- The trap here is treating CapEx like an operating expense; it is not an immediate income statement item.

## F. How do debt issuance and debt repayment affect the 3 statements?

Debt principal flows through financing, not operations. Issuing debt brings in cash and raises the debt balance; repaying principal uses cash and lowers the debt balance. The income statement is affected later through interest expense, not by principal itself.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '22px'}, 'flowchart': {'htmlLabels': true, 'nodeSpacing': 50, 'rankSpacing': 80, 'useMaxWidth': true}} }%%
flowchart TD
  subgraph F_ISS["Debt issuance"]
    F_I1["Issue debt"] --> F_B1["Debt up (BS)"]
    F_I1 -->|Source of cash| F_C1["Cash up (CFF and BS)"]
    F_B1 -->|later| F_IS1["Future interest expense up (IS)"]
  end

  subgraph F_REP["Debt repayment"]
    F_R1["Repay principal"] --> F_B2["Debt down (BS)"]
    F_R1 -->|Use of cash| F_C2["Cash down (CFF and BS)"]
    F_R1 --> F_NO["No immediate P&L effect"]
    F_B2 -->|later| F_IS2["Future interest expense down (IS)"]
  end

  classDef is fill:#dbeafe,stroke:#1d4ed8,color:#0f172a,stroke-width:1.5px;
  classDef cfs fill:#dcfce7,stroke:#15803d,color:#14532d,stroke-width:1.5px;
  classDef bs fill:#fef3c7,stroke:#b45309,color:#78350f,stroke-width:1.5px;
  classDef use fill:#fee2e2,stroke:#dc2626,color:#7f1d1d,stroke-width:1.5px;
  classDef source fill:#dcfce7,stroke:#16a34a,color:#14532d,stroke-width:1.5px;
  classDef note fill:#f8fafc,stroke:#64748b,color:#334155,stroke-width:1.5px;

  class F_I1,F_C1 source;
  class F_R1,F_C2 use;
  class F_B1,F_B2 bs;
  class F_IS1,F_IS2 is;
  class F_NO note;
```

Interview script:

- New debt issuance is a financing inflow, so cash goes up and debt on the balance sheet goes up.
- There is no immediate operating income statement benefit from issuing debt.
- The income statement effect comes later because more debt usually means more interest expense.
- Debt repayment is the reverse: cash goes down and debt goes down.
- Principal repayment does not run through the income statement.
- Lower debt usually means lower future interest expense.
- A common trap is mixing up principal and interest; principal hits financing, interest hits earnings and usually CFO.

## G. How does interest expense affect the 3 statements?

Interest expense is an income statement item driven by the debt balance and interest rate. It lowers pretax income and net income, usually reduces CFO through cash interest paid, and does not by itself change the debt principal balance.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '22px'}, 'flowchart': {'htmlLabels': true, 'nodeSpacing': 50, 'rankSpacing': 80, 'useMaxWidth': true}} }%%
flowchart LR
  subgraph G_BS["Balance Sheet"]
    G_DEBT["Debt balance"]
    G_PAY["Interest payable"]
    G_CASH["Cash down when paid"]
    G_RE["Retained earnings down"]
  end

  subgraph G_IS["Income Statement"]
    G_INT["Interest expense"] --> G_EBT["EBT down"]
    G_EBT --> G_TAX["Taxes down"]
    G_TAX --> G_NI["Net income down"]
  end

  subgraph G_CFS["Cash Flow Statement"]
    G_NI --> G_CFO["CFO lower via NI"]
    G_CPAY["Cash interest paid (usually CFO)"]
  end

  G_DEBT -->|rate x balance| G_INT
  G_INT -->|usually cash, not added back| G_CPAY
  G_CPAY -->|cash outflow| G_CASH
  G_NI --> G_RE
  G_INT -.->|if unpaid yet| G_PAY
  G_PAY -.->|Payable up = source now Payable down = use later| G_CPAY

  classDef is fill:#dbeafe,stroke:#1d4ed8,color:#0f172a,stroke-width:1.5px;
  classDef cfs fill:#dcfce7,stroke:#15803d,color:#14532d,stroke-width:1.5px;
  classDef bs fill:#fef3c7,stroke:#b45309,color:#78350f,stroke-width:1.5px;
  classDef use fill:#fee2e2,stroke:#dc2626,color:#7f1d1d,stroke-width:1.5px;

  class G_INT,G_EBT,G_TAX,G_NI is;
  class G_CFO cfs;
  class G_DEBT,G_PAY,G_CASH,G_RE bs;
  class G_CPAY use;
```

Interview script:

- Interest expense comes from the debt balance times the interest rate.
- It reduces EBT, which reduces taxes, and net income still falls on an after-tax basis.
- Because it is generally a real cash cost, you do not add it back like depreciation.
- Under the usual interview convention, cash interest paid sits in CFO.
- The debt principal balance does not change just because you recorded interest expense.
- If interest accrues but is not yet paid, interest payable goes up and cash is temporarily higher.
- The trap is saying debt goes down from interest expense alone; only principal repayment reduces debt.

## H. How do taxes flow through the 3 statements?

Tax expense on the income statement is not always equal to cash taxes paid. The balance sheet holds the timing difference in taxes payable and deferred tax accounts, and the cash flow statement reconciles accounting tax expense to actual cash paid.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '22px'}, 'flowchart': {'htmlLabels': true, 'nodeSpacing': 50, 'rankSpacing': 80, 'useMaxWidth': true}} }%%
flowchart LR
  subgraph H_IS["Income Statement"]
    H_PBT["Pretax income"] --> H_TEXP["Tax expense"]
    H_TEXP --> H_NI["Net income"]
  end

  subgraph H_BS["Balance Sheet"]
    H_TP["Taxes payable"]
    H_DT["DTA / DTL"]
    H_CASH["Cash down when taxes are paid"]
    H_RE["Retained earnings down"]
  end

  subgraph H_CFS["Cash Flow Statement"]
    H_NI --> H_CFO0["CFO starts with NI"]
    H_DTAJ["Deferred tax adjustment"]
    H_CFO["CFO after tax timing"]
    H_CFO0 --> H_CFO
    H_DTAJ --> H_CFO
  end

  H_TEXP -->|current tax| H_TP
  H_TEXP -->|timing differences| H_DT
  H_DT -->|non-cash tax timing| H_DTAJ
  H_TP -.->|Taxes payable up = source Taxes payable down = use| H_CFO
  H_TP -->|cash payment| H_CASH
  H_NI --> H_RE

  classDef is fill:#dbeafe,stroke:#1d4ed8,color:#0f172a,stroke-width:1.5px;
  classDef cfs fill:#dcfce7,stroke:#15803d,color:#14532d,stroke-width:1.5px;
  classDef bs fill:#fef3c7,stroke:#b45309,color:#78350f,stroke-width:1.5px;

  class H_PBT,H_TEXP,H_NI is;
  class H_CFO0,H_DTAJ,H_CFO cfs;
  class H_TP,H_DT,H_CASH,H_RE bs;
```

Interview script:

- Start with pretax income, apply tax expense, and that gets you to net income.
- But tax expense is accounting tax, not always cash tax.
- The current unpaid portion sits in taxes payable on the balance sheet.
- If taxes payable goes up, you recognized expense but paid less cash, so that is a source of cash.
- If taxes payable goes down, you paid more cash than current expense, so that is a use of cash.
- Deferred tax assets and liabilities capture timing differences between book and tax accounting.
- On the cash flow statement, you adjust net income for those timing differences to get to actual cash taxes.
