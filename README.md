### Digital Financial Product Adoption

**Who has moved beyond just having a bank account?**

**Author:** Karabo Sishuba

---

## Business Question

Many people around the world now have an account. But do they actually use it to pay for things digitally? This project looks at World Bank survey data to find out where the biggest gaps are, so a product or inclusion team can decide where to put effort next:

1. Opening more accounts, or
2. Getting existing account holders to use digital products.

**My answer:** It depends on the market. Poorer countries mainly still need accounts. Lower-middle-income countries already have accounts, but few people use them to pay. Richer countries are mostly past both problems.

---

## Project Summary

| | |
|---|---|
| **Dataset** | [World Bank Global Findex Database 2025](https://www.worldbank.org/en/publication/globalfindex) (country-level Excel file) |
| **Raw rows** | 8,577 |
| **Clean rows** | 32,448 |
| **Economies** | 162 across all years, 141 in 2024 |
| **Survey years** | 2011, 2014, 2017, 2021, 2024 (plus a small partial 2022 survey) |
| **Tools** | Excel, Power Query, PivotTables, Pivot Charts, slicers |
| **What I did** | 1) Cleaned the raw file with Power Query. 2) Built an Excel dashboard with five pages. 3) Wrote recommendations. |

All numbers below are for **2024** and are **weighted by adult population**, unless stated.

---

## Key Findings

| Market type | Income group | What I found | What to focus on |
|---|---|---|---|
| **Access** | Low income | 46% have an account, only 8% have paid a merchant digitally | Get people into an account (mobile money works best) |
| **Activation** | Lower-middle income | 70% have an account, only 20% pay merchants digitally | Get account holders to actually use it |
| **Deepening** | Upper-middle and high income | 83% to 95% have an account, 64% to 66% pay merchants digitally | Close the remaining gaps |

**Other things I found**

- Low-income countries are about half as likely to have an account as high-income countries (46% vs 95%), but about **eight times** less likely to have paid a merchant digitally (8% vs 64%).
- The biggest drop from "has an account" to "pays a merchant digitally" is in **lower-middle-income** countries (50.5 points), not low-income ones.
- In low-income countries, mobile money (31.8%) reaches more adults than a bank-type account (25.8%).
- The poorest 40% of people trail the richest 60% by about 19 points on digital use.
- Women trail men by only 4 points on accounts, but by 12 points on mobile money.
- Upper-middle income looks as good as high income, but only because of China (see Finding 3 below).

---

## Formulas Used

The data is stored as shares of adults between 0 and 1 (for example 0.46 = 46%).

**1. Weighted value** (a column I added in Power Query)

```
Weighted value = Value x Adult population
```

This gives roughly the number of adults who have the product.

**2. Weighted adoption** (the main number used in the dashboard)

```
Weighted adoption = Total of Weighted value / Total of Adult population
```

*Example:* Country A has 80% adoption and 10 million adults. Country B has 40% adoption and 30 million adults.

```
(0.80 x 10m + 0.40 x 30m) / (10m + 30m) = 20m / 40m = 50%
```

A plain average would say 60%, which is too high because the bigger country is the lower one. In the PivotTable this is a calculated field: `='Weighted value' / 'Adult population'`.

**3. Gap between groups**

```
Gap (pts) = Group value - Reference value
```

A negative number means the group is behind. Example: women's mobile money is 12.4 points below men's, so the gap is -12.4. I compared women vs men, poorest 40% vs richest 60%, and rural vs urban.

**4. Drop-off along the adoption ladder**

```
Drop-off (pts) = Account (any) - Digital merchant payment
```

Example, lower-middle income: 70.4% - 19.9% = **50.5 points**.

**5. Economies reporting**

```
Economies reporting = Count of Value where Segment type = "all"
```

I only count the "all adults" rows so each country is counted once, not once for every group (gender, age and so on).

---

## Data Limitations

Every dataset has weak spots. These are the ones that affect how far the findings in this project can be trusted, and what I did about each.

### About what the data is

| Limitation | What it means | How I handled it |
|---|---|---|
| **Shares, not people** | Each row is the percentage of adults in a group, not a record for one person | I only compare groups, and I never claim anything about individuals |
| **No individual journeys** | I cannot tell if the same person who has an account also pays a merchant digitally | I describe "drop-off" between groups, not people moving between steps |
| **Adults means 15 and over** | The survey target group starts at age 15, not 18 | I use the word "adults" as the survey does, and note the age |
| **Descriptive, not causal** | The data shows where gaps are, not why they exist | I avoid words like "because" and list causes as a next step |
| **Snapshots only** | There are five survey years with changing coverage, so there is not enough to forecast | I describe past change and make no predictions |

### About how the data was collected

| Limitation | What it means | How I handled it |
|---|---|---|
| **Survey error** | Each country has about 1,000 respondents, so figures can be off by about 2 to 5 points (South Africa about 3.7). Cuts such as "women only" use about half the sample, so they are less precise | I treat gaps of one or two points as noise and do not over-read close rankings |
| **No statistical tests** | I did not test whether differences are statistically significant | I only highlight large gaps, and I say this clearly |
| **Different survey methods** | Most low- and middle-income countries were surveyed face to face, most high-income ones by phone. China, Algeria, Iran, Libya, Mauritius and Ukraine used a shorter phone questionnaire | I flag China's result as less reliable |
| **Some people left out** | Some country samples exclude up to 30% of the population for security or access reasons (for example Ethiopia) | I mention it, but I cannot correct for it |
| **"Don't know" counted as "no"** | Refused or unsure answers are coded as "no", so adoption is slightly understated | I note that figures are likely a little low |

### About coverage

| Limitation | What it means | How I handled it |
|---|---|---|
| **Newer products cover fewer countries** | In 2024, accounts cover 141 economies, digital payments and digitally enabled accounts 98, and mobile money 81 | I always say "among reporting economies" and never "global" |
| **Different start years** | Mobile money starts in 2014, merchant payments in 2021 and digitally enabled accounts in 2024, so there is no long trend for the newest products | The trend table shows "n/a" where the question was not asked |
| **Countries change between years** | 123 economies were in the 2021 account data and 141 in 2024, so a headline change mixes real growth with new countries joining | I flag this and list a like-for-like trend as a next step |
| **2022 is a partial survey** | Only 16 economies were surveyed, so including it would show a fake drop | I flagged it in Power Query and left it out of trend lines |
| **Small groups** | Only 16 low-income economies report merchant payments | I rate the low-income recommendation as medium confidence |

### About the way I calculated things

| Limitation | What it means | How I handled it |
|---|---|---|
| **Weighting favours big countries** | China and India move every population-weighted figure | I show the China effect directly and use economy averages for rankings |
| **Rankings are fragile** | With about 1,000 respondents per country, countries close together in rank cannot really be told apart | I give ranks for context only, not as firm conclusions |
| **Blanks are not zeros** | A blank means the country was not asked, not that adoption is zero | I dropped blanks instead of filling them in |
| **Excel has no distinct count** | Without the Data Model, Excel cannot count unique countries easily | I count only the "all adults" rows so each country is counted once |
| **Label mapping to confirm** | I matched `dig.acc` to "digitally enabled account" by its label. Digitally enabled means the account *can* be used digitally, not that it is | The mapping should be confirmed against the country-level codebook |

### What this means for the reader

Use these results to decide **where to look and where to focus effort**. Do not use them to prove **why** a gap exists, to rank countries precisely, or to predict future adoption.

---

## Recommendations

### 1. Low-income markets: focus on access, using mobile money

46% of adults have an account, and mobile money (31.8%) reaches more people than a bank-type account (25.8%). **Recommendation:** lead with mobile-money onboarding rather than branch or bank products. *Confidence: medium (only 16 low-income economies report merchant payments).*

### 2. Lower-middle-income markets: focus on activation

This group has the biggest drop-off (70.4% have an account, 19.9% pay merchants digitally). **Recommendation:** put effort into merchant acceptance and using wallets at shops, because the accounts already exist. *Confidence: medium to high (40 economies report merchant payments).*

### 3. Do not treat upper-middle income as "done"

Upper-middle income shows 66.1% merchant payment vs 64.5% for high income, but China is 62% of that group's population. Without China, the figure is 44.3%. Countries inside the group also differ a lot: Brazil 60%, Türkiye 51%, Mexico 26%. **Recommendation:** look at these countries one by one and do not use the group average as a benchmark. *Confidence: high that China drives the average.*

### 4. Match the fix to the gap

| Gap (points) | Account | Mobile money | Digitally enabled | Merchant | Saved |
|---|---|---|---|---|---|
| Women vs men | -4.3 | **-12.4** | -9.6 | -6.4 | -4.7 |
| Poorest 40% vs richest 60% | -10.6 | -18.2 | **-19.2** | **-18.9** | **-19.6** |
| Rural vs urban | -4.5 | -10.6 | -10.6 | **-11.0** | -7.2 |

- **Income is the widest gap** on every digital product (about 19 points).
- **Women's gap is mostly a mobile money gap**, so target women's mobile money rather than accounts in general.
- **Rural adults trail by about 11 points on digital use**, roughly double their account gap. This points to acceptance and connectivity rather than account opening.
- **Borrowing shows almost no gap** by income or location, so credit is not where the inequality is.

*Confidence: medium to high for income, medium for the others.*

### 5. Growth is slowing for accounts but not mobile money

Account ownership grew by about 11, 8, 7 and then only 2 points across the survey years. Mobile money grew from 4.0% (2014) to 28.1% (2024). Merchant payments barely moved (36.8% to 38.8%). **Recommendation:** extra effort on opening accounts has diminishing returns outside low-income markets, and merchant payments are the stage that has stalled. *Confidence: medium (more countries joined the survey over time, which affects the trend).*

### 6. South Africa: strong on accounts, room to grow on payments

South Africa has 81.1% account ownership, and 67.8% have a digitally enabled account, but only 46.9% pay merchants digitally, a 20.9-point gap. It ranks #3 of 35 in Sub-Saharan Africa on merchant payments, but only #15 of 36 among upper-middle-income peers. Mobile money is 31.6%, so adoption is bank-led. **Recommendation:** focus on card and app use at the till rather than mobile money, and compare against upper-middle-income peers, not just African countries. *Confidence: medium (about 1,000 interviews, margin about 3.7 points, so middle-of-table ranks are not reliable).*

---

## What I Would Do Next

1. Add a "without China" view for upper-middle income to the dashboard.
2. Show a fair trend using only countries surveyed in both years next to the headline trend. On those countries, account ownership rose from 76.7% to 80.1% (2021 to 2024) and merchant payments from 36.3% to 39.9%, which is more growth than the headline shows.
3. Add the cause of the gaps (for example phone access or merchant acceptance) using other data, since this dataset cannot explain why gaps exist.

---

## Phase 1 - Cleaning the Data (Power Query)

**Problems with the raw file**

- Blanks were stored as the text `NA`, so number columns loaded as text.
- The file mixed 162 real economies with 12 World Bank summary rows (World, regions, income groups).
- The data was spread across hundreds of columns.

**Steps I took**

| # | Step | Why |
|---|---|---|
| 1 | Loaded the `Data` sheet as a connection-only query (`raw_findex`) | The raw data stays untouched |
| 2 | Replaced `NA` with blank | So numbers load as numbers |
| 3 | Split the 684 summary rows into their own table (`agg_reference`) | Mixing them in would double-count |
| 4 | Kept 15 columns: 8 descriptors and 7 indicators | Everything else was out of scope |
| 5 | Renamed columns and set data types (`Year` as text) | So the PivotTable never adds years together |
| 6 | Flagged 2022 as a partial wave | So I can leave it out of trend lines |
| 7 | Unpivoted the 7 indicators into `Indicator` and `Value` | One long table that works with one slicer |
| 8 | Added `Product stage`, readable labels and `Weighted value` | Needed for the weighted calculation |
| 9 | Loaded the results as Excel tables | Ready to refresh |

**The 7 indicators I kept**

| Stage | Indicator | Economies in 2024 |
|---|---|---|
| 1 Access | Account (any) | 141 |
| 1 Access | Financial institution account | 141 |
| 2 Mobile | Mobile money account | 81 |
| 3 Digital use | Digitally enabled account | 98 |
| 4 Merchant | Digital merchant payment | 98 |
| 5 Credit & savings | Borrowed any money | 98 |
| 5 Credit & savings | Saved any money | 98 |

### Power Query (M) code

`FilePath` is a text parameter that holds the location of the Excel file.

**`raw_findex`**

```m
let
    Source        = Excel.Workbook(File.Contents(FilePath), null, true),
    Data_Sheet    = Source{[Item = "Data", Kind = "Sheet"]}[Data],
    PromotedCodes = Table.PromoteHeaders(Data_Sheet, [PromoteAllScalars = true]),
    NoLabelRow    = Table.Skip(PromotedCodes, 1),
    NoNA          = Table.ReplaceValue(NoLabelRow, "NA", null, Replacer.ReplaceValue, Table.ColumnNames(NoLabelRow)),
    NoBlankRows   = Table.SelectRows(NoNA, each [countrynewwb] <> null)
in
    NoBlankRows
```

**`agg_reference`** (the 12 summary groups)

```m
let
    Source = raw_findex,
    Aggs   = Table.SelectRows(Source, each [regionwb24_hi] = null)
in
    Aggs
```

**`tbl_findex`** (the final clean table)

```m
let
    Source      = raw_findex,
    Countries   = Table.SelectRows(Source, each [regionwb24_hi] <> null),
    Descriptors = {"countrynewwb","codewb","year","pop_adult","regionwb24_hi",
                   "incomegroupwb24","group","group2"},
    Indicators  = {"account.t.d","fiaccount.t.d","mobileaccount.t.d","dig.acc",
                   "merchant.pay","borrow.any.t.d","save.any.t.d"},
    Kept        = Table.SelectColumns(Countries, Descriptors & Indicators),
    Renamed     = Table.RenameColumns(Kept, {
                    {"countrynewwb","Economy"}, {"codewb","Code"}, {"year","Year"},
                    {"pop_adult","Adult population"}, {"regionwb24_hi","Region"},
                    {"incomegroupwb24","Income group"}, {"group","Segment type"},
                    {"group2","Segment"}}),
    Typed       = Table.TransformColumnTypes(Renamed,
                    {{"Year", type text}, {"Adult population", type number}}
                    & List.Transform(Indicators, each {_, type number}), "en-US"),
    WaveType    = Table.AddColumn(Typed, "Wave type",
                    each if [Year] = "2022" then "Partial wave (16 economies)" else "Full wave", type text),
    DescCols    = {"Economy","Code","Year","Adult population","Region",
                   "Income group","Segment type","Segment","Wave type"},
    Long        = Table.UnpivotOtherColumns(WaveType, DescCols, "Indicator", "Value"),
    NoBlanks    = Table.SelectRows(Long, each [Value] <> null),
    StageMap    = [#"account.t.d"="1 Access", #"fiaccount.t.d"="1 Access",
                   #"mobileaccount.t.d"="2 Mobile", #"dig.acc"="3 Digital use",
                   #"merchant.pay"="4 Merchant", #"borrow.any.t.d"="5 Credit & savings",
                   #"save.any.t.d"="5 Credit & savings"],
    LabelMap    = [#"account.t.d"="Account (any)",
                   #"fiaccount.t.d"="Financial institution account",
                   #"mobileaccount.t.d"="Mobile money account",
                   #"dig.acc"="Digitally enabled account",
                   #"merchant.pay"="Digital merchant payment",
                   #"borrow.any.t.d"="Borrowed any money",
                   #"save.any.t.d"="Saved any money"],
    Staged      = Table.AddColumn(NoBlanks, "Product stage",
                    each Record.Field(StageMap, [Indicator]), type text),
    Labelled    = Table.TransformColumns(Staged,
                    {{"Indicator", each Record.Field(LabelMap, _), type text}}),
    Weighted    = Table.AddColumn(Labelled, "Weighted value",
                    each [Value] * [Adult population], type number)
in
    Weighted
```

### Checks I ran

| Check | Expected | Result |
|---|---|---|
| Summary rows in `agg_reference` | 684 | 684 |
| Economies in `tbl_findex` | 162 | 162 |
| Rows in `tbl_findex` | 32,448 | 32,448 |
| Rows excluding 2022 | 31,584 | 31,584 |
| Values outside 0 to 1 | 0 | 0 |

### Cleaning decisions

- **Summary rows were separated, not deleted**, so country figures stay clean but the World Bank's own totals are still available.
- **Blanks were dropped, not filled with zero.** A blank means the country was not asked, and zero would invent data.
- **2022 was flagged, not removed**, because it only covers 16 economies and would show a fake drop in trend lines.

---

## Phase 2 - Excel Dashboard

Built from `tbl_findex` with PivotTables, Pivot Charts and four slicers (Indicator, Region, Income group, Year).

| Sheet | What it shows |
|---|---|
| `Overview` | Headline numbers and the main chart |
| `P1_Trend` | How adoption changed from 2011 to 2024 |
| `P2_Ladder` | Account, digital account and merchant payment by income group, with drop-off |
| `P3_Equity` | Gaps for women vs men, poorest vs richest, rural vs urban |
| `P4_League` | Top and bottom 10 economies, plus a South Africa spotlight |

### Results tables

**Trend over time (2022 left out)**

| Indicator | 2011 | 2014 | 2017 | 2021 | 2024 |
|---|---|---|---|---|---|
| Account (any) | 50.6% | 61.3% | 69.0% | 76.2% | 78.0% |
| Mobile money account | n/a | 4.0% | 8.1% | 18.3% | 28.1% |
| Digital merchant payment | n/a | n/a | n/a | 36.8% | 38.8% |
| Digitally enabled account | n/a | n/a | n/a | n/a | 52.1% |

*n/a means the question was not asked that year.*

**Adoption ladder by income group (2024)**

| Stage | Low | Lower middle | Upper middle | High |
|---|---|---|---|---|
| Account (any) | 46.4% | 70.4% | 83.0% | 94.9% |
| Mobile money account | 31.8% | 25.4% | 31.9% | 50.7% |
| Digitally enabled account | 34.7% | 36.8% | 73.2% | 72.6% |
| Digital merchant payment | 8.5% | 19.9% | 66.1% | 64.5% |
| Drop-off, account to merchant (pts) | 37.9 | 50.5 | 16.9 | 30.4 |

**South Africa (2024)**

| Indicator | Value | Rank, all economies | Rank, upper-middle income | Rank, Sub-Saharan Africa |
|---|---|---|---|---|
| Account (any) | 81.1% | #60 of 141 | #13 of 37 | #4 of 35 |
| Mobile money account | 31.6% | #42 of 81 | #13 of 24 | #26 of 34 |
| Digitally enabled account | 67.8% | #18 of 98 | #7 of 36 | #6 of 35 |
| Digital merchant payment | 46.9% | #24 of 98 | #15 of 36 | #3 of 35 |

---

## Files in This Repository

| File | Description |
|---|---|
| `data/GlobalFindexDatabase2025.xlsx` | Raw World Bank file, untouched |
| `queries/raw_findex.m` | Power Query: load the raw sheet and clean `NA` |
| `queries/agg_reference.m` | Power Query: the 12 summary groups |
| `queries/tbl_findex.m` | Power Query: the final clean table |
| `digital_adoption_analysis.xlsx` | Clean tables and the dashboard |
| `README.md` | This file |

---

## Source

World Bank, *The Global Findex Database 2025: Connectivity and Financial Inclusion in the Digital Economy*. Country-level database.

*Author: Karabo Sishuba*
