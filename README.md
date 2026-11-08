# UK Data for Agents

Hosted MCP server with 380 ready-to-use tools for AI agents: UK Companies House and KYB, sanctions screening, public tenders, property prices and EPCs, mortgage and UK business calculators, Parliament, vehicles and MOT, travel advice, weather, FX, documents and more.

**Hosted, no install, no API keys of your own.** Point any MCP client at one URL. Every data source is already wired in, and every tool is tested against its live source on a rolling schedule.

- Remote MCP (Streamable HTTP): `https://ukdata.reliness.co.uk/mcp`
- One family at a time (smaller tool lists): `https://ukdata.reliness.co.uk/mcp/<family>`
- REST: `GET https://ukdata.reliness.co.uk/v1/<tool>?param=value`
- Website and docs: https://ukdata.reliness.co.uk

## Start free

Call any tool straight away with no key: every caller gets a free daily allowance. For more, get a free key with 300 credits:

```bash
curl -X POST https://ukdata.reliness.co.uk/keys -H 'content-type: application/json' -d '{"email":"you@example.com"}'
```

Then send `Authorization: Bearer <key>`. Credit packs: £10 for 2,000 credits, £40 for 10,000, £150 for 50,000. Most tools cost 1 credit.

## Connect

**Claude Desktop / Claude Code / Cursor / any MCP client**

```json
{
  "mcpServers": {
    "uk-data": {
      "url": "https://ukdata.reliness.co.uk/mcp/uk-companies",
      "headers": { "Authorization": "Bearer ukd_your_key" }
    }
  }
}
```

Swap `uk-companies` for any family below, or use `/mcp` for everything plus `tool_search` and `call_tool`.

**Try it without a client**

```bash
curl "https://ukdata.reliness.co.uk/v1/company_search?query=tesco"
curl "https://ukdata.reliness.co.uk/v1/mortgage_repayment?propertyPrice=300000&deposit=60000"
curl "https://ukdata.reliness.co.uk/v1/convert_currency?amount=100&from_currency=GBP&to_currency=USD"
```

## Why this one

- **No setup.** Most UK data MCP servers run locally and need your own Companies House, EPC or HMRC keys. This one is hosted and the keys are ours.
- **One job per tool**, named and described the way agents ask, with clear errors and refunds when a source fails.
- **Checked continuously.** Every tool runs against its live source on a rolling schedule.
- **Agent-standard names work too.** Calls such as `convert_currency`, `calculate_loan_payment`, `get_definition`, `whois` and `get_current_time` are answered by the matching tool.

## Tool families

### UK Companies House (`uk-companies`)

Company search, profiles, officers, owners, filings, charges, insolvency, disqualified directors and full KYB checks from the official register.

`https://ukdata.reliness.co.uk/mcp/uk-companies`

`company_search`, `company_profile`, `company_officers`, `company_pscs`, `company_filings`, `companies_incorporated`, `officer_appointments`, `disqualified_officers`, `company_charges`, `company_insolvency`, `kyb_check`

### UK due diligence (`uk-due-diligence`)

Deeper checks on UK companies, financial firms, advisers and charities: filed accounts figures, full FCA register checks on firms and individuals, and charity search and profiles. Use before paying, partnering with, investing in or donating to an organisation.

`https://ukdata.reliness.co.uk/mcp/uk-due-diligence`

`company_accounts`, `fca_firm`, `fca_individual`, `charity_search`, `charity_profile`

### Sanctions screening (`sanctions-screening`)

Screen people, companies and ships against the UK (FCDO/OFSI), US (OFAC SDN and Consolidated), EU and UN sanctions lists, refreshed daily. One general screen plus checks specialised by type and by list.

`https://ukdata.reliness.co.uk/mcp/sanctions-screening`

`sanctions_screen`, `sanctions_check_person`, `sanctions_check_company`, `sanctions_check_ship`, `ofac_check`, `uk_sanctions_check`, `eu_sanctions_check`, `un_sanctions_check`

### UK public tenders (`uk-tenders`)

Open tenders and contract awards from Find a Tender and Contracts Finder with values, buyers, winners and deadlines.

`https://ukdata.reliness.co.uk/mcp/uk-tenders`

`tenders_search`

### UK property (`uk-property`)

Land Registry sold prices and Energy Performance Certificates by postcode, street or address.

`https://ukdata.reliness.co.uk/mcp/uk-property`

`price_paid`, `epc_search`

### UK business calculators (`uk-business-calculators`)

The arithmetic agents get wrong: VAT, stamp duty, statutory late payment interest, redundancy pay, holiday entitlement, statutory sick pay, with dated rate tables.

`https://ukdata.reliness.co.uk/mcp/uk-business-calculators`

`vat`, `stamp_duty`, `late_payment_interest`, `redundancy_pay`, `holiday_entitlement`, `mortgage_repayment`, `loan_repayment`, `statutory_sick_pay`

### Vehicle lookups (`vehicles`)

Look up a vehicle by UK or Dutch number plate or decode any VIN: make, model, MOT history, mileage checks, engine, fuel, weights, recalls and safety kit, from official sources.

`https://ukdata.reliness.co.uk/mcp/vehicles`

`nl_vehicle`, `vin_decode`, `uk_vehicle`, `uk_mot_history`, `uk_mileage_check`

### UK Parliament Votes (Commons and Lords Divisions) (`uk-parliament-votes`)

How MPs and peers voted, straight from the official UK Parliament votes record: find any Commons or Lords division, see the result and party split, list every member on each side, and pull an individual MP's or peer's voting record.

`https://ukdata.reliness.co.uk/mcp/uk-parliament-votes`

`commons_division_search`, `commons_recent_divisions`, `commons_division_result`, `lords_division_search`, `lords_division_result`

### UK Parliament Members, Constituencies and Election Results (`uk-parliament-people`)

Live answers from the UK Parliament Members API: the latest result and election history for any constituency, who holds each Cabinet-level post today, party seat numbers in the Commons and Lords on any date, and an MP's or peer's official contact details, parliamentary career and Register of Interests entries.

`https://ukdata.reliness.co.uk/mcp/uk-parliament-people`

`constituency_election_result`, `constituency_search`, `mp_contact_details`, `member_career_history`, `member_registered_interests`, `cabinet_ministers`, `commons_party_seats`, `lords_party_composition`

### UK Parliament Bills, Treaties and Statutory Instruments (`uk-parliament-legislation`)

Where a UK bill, treaty or statutory instrument is in Parliament: stages and dates, sponsors, published documents, amendments and decisions, Royal Assent. Live from the official UK Parliament APIs, so answers reflect what Parliament records today rather than stale training data.

`https://ukdata.reliness.co.uk/mcp/uk-parliament-legislation`

`bill_search`, `bill_status`, `bill_stages_timeline`, `bill_documents`, `bill_amendments`, `bills_recently_updated`, `acts_recent_royal_assent`, `treaty_search`, `statutory_instrument_search`

### UK FCDO Foreign Travel Advice (`travel-safety`)

The UK government's official travel advice for every country it covers, live from GOV.UK: FCDO warnings, entry requirements, safety, health and the latest changes, split into the parts travellers and insurers actually ask about.

`https://ukdata.reliness.co.uk/mcp/travel-safety`

`travel_advice_country`, `travel_advice_entry_requirements`, `travel_advice_safety`, `travel_advice_health`, `travel_advice_warnings_insurance`, `travel_advice_recent_updates`, `travel_advice_countries`

### UK food hygiene ratings (`uk-food-hygiene`)

Every rated food business from the Food Standards Agency with scores, addresses and coordinates.

`https://ukdata.reliness.co.uk/mcp/uk-food-hygiene`

`food_hygiene_search`

### UK insolvency notices (`uk-insolvency`)

Winding up, administration, liquidation and bankruptcy notices from The Gazette.

`https://ukdata.reliness.co.uk/mcp/uk-insolvency`

`insolvency_notices`

### UK places (`uk-places`)

Postcode lookup, street-level crime, flood warnings, grid carbon intensity and bank holidays.

`https://ukdata.reliness.co.uk/mcp/uk-places`

`postcode_lookup`, `crime_nearby`, `flood_warnings`, `carbon_intensity`, `bank_holidays`

### Environment Agency river levels, flow, rainfall, tide and groundwater (England) (`uk-water-levels`)

Live readings, usually every 15 minutes, from Environment Agency gauges across England: river levels against their normal range and records, river flow, rain gauge totals, coastal and tidal levels, and groundwater boreholes. Answers "is the river high or rising", "how much rain fell" and "is the tide in" in plain fields with units.

`https://ukdata.reliness.co.uk/mcp/uk-water-levels`

`river_level_now`, `river_level_history`, `river_stations_on_river`, `river_level_record`, `river_flow_now`, `rainfall_last_24h`

### Defra UK-AIR live air pollution (`air-quality`)

Hourly measured air pollution from the UK's official automatic monitoring network (Defra AURN, via UK-AIR): nearest monitors, the latest NO2, PM2.5, PM10 and ozone readings with their Daily Air Quality Index band and health advice, and up to 7 days of hourly history.

`https://ukdata.reliness.co.uk/mcp/air-quality`

`air_quality_stations_near`, `no2_level_near`, `pm25_level_near`, `pm10_level_near`, `ozone_level_near`, `air_quality_index_near`, `air_pollutant_history`

### Catalogue (`catalogue`)

Find the right tool for a need across every native family and every imported API, then call it by name from one endpoint.

`https://ukdata.reliness.co.uk/mcp/catalogue`

`tool_search`, `call_tool`, `list_apis`

### Federal Reserve Board Releases (`central-banks-rates`)

Official US Federal Reserve decisions and schedules straight from the Board of Governors: the latest FOMC rate decision with vote split and dissenters, meeting dates with announcement times in any time zone, minutes, speeches, testimony and enforcement actions. Policy announcements from the central bank itself, not market quotes.

`https://ukdata.reliness.co.uk/mcp/central-banks-rates`

`fomc_meeting_dates`, `fomc_minutes_latest`, `fed_monetary_policy_releases`, `fed_speeches_latest`, `fed_repo_operations_results`

### Code Utilities (`code-utilities`)

Code utilities: deterministic string, list, number and validation routines (palindromes, sorting, searching, parentheses, IP validation, merging)

`https://ukdata.reliness.co.uk/mcp/code-utilities`

`is_valid_ip_address`, `find_max_subarray_sum`, `merge_dictionaries`, `find_kth_smallest`, `count_bits`, `binary_search`, `reverse_string`, `min_meeting_rooms`, `find_next_greater_element`, `binary_addition`, `is_palindrome`, `sort_numbers`, `find_pairs_with_sum`, `is_perfect_square`, `find_n_largest`, `is_valid_parentheses`, `find_minimum_rotated_sorted_array`, `flatten_list`, `is_anagram`, `find_first_non_repeating_char`, `find_equilibrium_index`, `find_missing_number`, `is_power`, `find_longest_word`, `can_attend_meetings`, `is_rotation`, `find_peak_element`, `find_duplicate_number`, `is_sum_of_cubes`, `validate_sudoku`, `find_majority_element`, `merge_sorted_lists`

### Compliance and finance checks (`compliance-finance-checks`)

Legal Entity Identifier lookups with parent companies (GLEIF), IBAN and UK sort code checks.

`https://ukdata.reliness.co.uk/mcp/compliance-finance-checks`

`lei_lookup`, `iban_validate`

### Words and definitions (`countries-words`)

Quick reference answers: a country's capital, currency, calling code, languages, neighbours and population, plus rhymes, synonyms, related words and dictionary definitions.

`https://ukdata.reliness.co.uk/mcp/countries-words`

`word_definition`, `word_pronunciation`

### Software Security & Package Popularity (`dev-security`)

Look up software vulnerabilities (CVEs) from the US National Vulnerability Database, and check package popularity via download statistics for npm (JavaScript), PyPI (Python), and Crates.io (Rust).

`https://ukdata.reliness.co.uk/mcp/dev-security`

`cve_lookup`, `npm_stats`, `pypi_stats`, `crate_stats`

### Document maker (`documents`)

Turn markdown or rows into real files an agent can hand to a person: Word, CSV, print-ready HTML.

`https://ukdata.reliness.co.uk/mcp/documents`

`make_docx`, `make_csv`, `make_print_html`

### BEA Release Schedule (`economic-calendar`)

Official US release dates and times for the economic data that moves markets (GDP, PCE inflation, trade, corporate profits), straight from the publishing agency and converted to the user's time zone. These tools read the US Bureau of Economic Analysis release schedule files, so answers to "when is GDP out" or "what time is PCE in London" come from BEA itself rather than a third-party calendar.

`https://ukdata.reliness.co.uk/mcp/economic-calendar`

`next_gdp_release`, `next_pce_inflation_release`, `next_corporate_profits_release`, `bea_release_dates_for_year`, `next_cpi_release`, `next_jobs_report_release`, `next_ppi_release`, `next_jolts_release`, `next_eci_release`

### Eurostat EU country statistics (`economics-statistics`)

Official Eurostat headline figures for any EU, EFTA or candidate country: inflation (overall and by spending category), unemployment, GDP growth, government debt and deficit, minimum wages, house prices and household electricity prices. One country per call, recent periods only, with Eurostat flags such as estimated or provisional kept.

`https://ukdata.reliness.co.uk/mcp/economics-statistics`

`eu_inflation_rate`, `eu_unemployment_rate`, `eu_youth_unemployment_rate`, `eu_gdp_growth`, `eu_government_debt_ratio`, `eu_government_deficit`, `eu_minimum_wage`, `eu_house_price_growth`, `eu_household_electricity_price`

### Email and domain checks (`email-domain`)

Is this address deliverable, disposable, a role address? Does this domain resolve, accept mail, have SPF and DMARC?

`https://ukdata.reliness.co.uk/mcp/email-domain`

`email_check`, `domain_check`

### Everyday Calculators (`everyday-calculators`)

Everyday calculators: tips, discounts, ages, BMI, calorie needs, grades and GPA, fuel costs, dates

`https://ukdata.reliness.co.uk/mcp/everyday-calculators`

`calculate_grade`, `is_leap_year`, `calculate_gpa`, `batting_average`, `calculate_age`, `calculate_bmi`, `calculate_tip`, `calculate_calorie_intake`, `format_date`

### Finance Formulas (`finance-formulas`)

Finance formulas: compound and simple interest, investment growth and returns, future value, CAGR, dividends, discounted prices, tax at a rate

`https://ukdata.reliness.co.uk/mcp/finance-formulas`

`calculate_discounted_price`, `calculate_investment_return`, `future_investment_value`, `calculate_interest`, `calculate_discount`, `calculate_tax`, `project_investment_growth`, `compound_interest`, `cagr`, `calculate_dividend_per_share`

### Generators (`generators`)

Generators: secure passwords, random numbers and strings, colours, usernames, dice and card draws

`https://ukdata.reliness.co.uk/mcp/generators`

`draw_cards`, `generate_random_color`, `generate_password`, `generate_random_number`, `generate_username`, `generate_random_string`

### Clinical trials (`health-research`)

Search ClinicalTrials.gov by condition, drug, location and status, and get full trial details: eligibility, phase, sponsor, sites.

`https://ukdata.reliness.co.uk/mcp/health-research`

`clinical_trials`

### Protein facts (UniProt Knowledgebase) (`life-sciences`)

Research-grade protein reference data from UniProt, the world's main curated protein database run by EMBL-EBI, SIB and PIR: find proteins, map genes to proteins, and pull function, disease links, sequences, cell location and 3D structures. Built for students, researchers and biotech teams.

`https://ukdata.reliness.co.uk/mcp/life-sciences`

`protein_for_gene`, `protein_sequence`, `protein_3d_structures`

### Markets and EU (`markets-eu`)

SEC EDGAR full-text filings search, EU TED tenders, World Bank indicators.

`https://ukdata.reliness.co.uk/mcp/markets-eu`

`sec_filings`, `eu_tenders`, `world_bank`

### Maths and working days (`maths-dates`)

Safe maths evaluation and list statistics, and UK working-day arithmetic using official bank holidays.

`https://ukdata.reliness.co.uk/mcp/maths-dates`

`calculate`, `working_days`

### Maths Statistics (`maths-statistics`)

Maths and statistics: averages, spread, tests, regression, calculus, primes, factorials, Fibonacci, combinatorics, probability, geometry, distances

`https://ukdata.reliness.co.uk/mcp/maths-statistics`

`is_power_of_two`, `dice_roll_probability`, `polygon_area_shoelace`, `cosine_similarity`, `greatest_common_divisor`, `linear_regression_prediction`, `least_common_multiple`, `calculate_median`, `euclidean_distance`, `fibonacci`, `chi_square_independence_test`, `create_histogram`, `calculate_clock_angle`, `factorial`, `calculate_distance`, `calculate_area`, `calculate_standard_deviation`, `average`, `is_prime`, `solve_quadratic`, `permutation_count`, `probability_consecutive_rolls`

### US FDA medical devices, food and veterinary safety (openFDA) (`medicines-drugs`)

Medicine names, label text, safety reports, recalls, shortages and approvals from official regulators and the US National Library of Medicine. Factual reference data only, never medical advice.

`https://ukdata.reliness.co.uk/mcp/medicines-drugs`

`fda_device_recalls`, `fda_device_510k_clearances`, `fda_device_pma_approvals`, `fda_device_classification`, `fda_device_problem_reports`, `fda_supplement_reactions`, `fda_pet_drug_reactions`, `fda_drug_side_effects_reported`, `fda_drug_shortages`, `fda_ndc_lookup`, `drug_name_match`, `drug_spelling_suggest`, `drug_brand_names`, `drug_generic_ingredient`, `ndc_status`, `drug_listed_uses`, `drug_contraindicated_conditions`, `drug_pharmacologic_class`

### Money and time (`money-time`)

FX reference rates, public holidays for 100+ countries, current time and conversions by IANA zone.

`https://ukdata.reliness.co.uk/mcp/money-time`

`fx_rates`, `public_holidays`, `time_now`, `convert_time`

### News and feeds (`news-feeds`)

Worldwide news search by keyword and time window, Hacker News, and any RSS or Atom feed as JSON.

`https://ukdata.reliness.co.uk/mcp/news-feeds`

`news_search`, `hacker_news`, `rss_read`

### CDC Disease and Health Counts (`public-health-counts`)

Official US public health counts straight from CDC's open-data API: weekly notifiable disease cases (measles, whooping cough, mpox and 100+ more), hospital admissions for flu, COVID-19 and RSV, and provisional drug overdose deaths, with as-of dates and missing values kept explicit.

`https://ukdata.reliness.co.uk/mcp/public-health-counts`

`flu_hospital_admissions_weekly`, `covid_hospital_admissions_weekly`, `rsv_hospital_admissions_weekly`, `drug_overdose_deaths_12mo`

### Open Trivia Database quiz questions (`quiz-trivia`)

Ready-made, human-checked quiz questions with answers from the Open Trivia Database, by category and difficulty: multiple-choice or true/false, for pub quizzes, classrooms, team events and games.

`https://ukdata.reliness.co.uk/mcp/quiz-trivia`

`trivia_questions`, `trivia_true_false`, `trivia_categories`, `trivia_question_count`

### Reference (`reference`)

Wikipedia summaries in any language, books by ISBN or search (Open Library), food products by barcode (Open Food Facts), IP address ownership, unit conversion and money formatting with amounts in words.

`https://ukdata.reliness.co.uk/mcp/reference`

`wikipedia_summary`, `book_lookup`, `product_barcode`, `ip_lookup`, `convert_units`, `format_money`

### Research papers (`research-papers`)

Search 250 million scholarly works across OpenAlex, Crossref, arXiv and PubMed; resolve any DOI.

`https://ukdata.reliness.co.uk/mcp/research-papers`

`papers_search`, `arxiv_search`, `pubmed_search`, `doi_lookup`

### Science Formulas (`science-formulas`)

Science formulas: physics, chemistry and biology calculations such as velocity, fields, energy, resistance, growth and density

`https://ukdata.reliness.co.uk/mcp/science-formulas`

`project_population`, `calculate_electric_field`, `calculate_cell_density`, `calculate_bacterial_growth`, `calculate_final_velocity`, `potential_energy`, `wire_resistance`

### Is it down? Official service status (`service-status`)

Is a major online service down right now? Get live status updates, active incident reports, and affected component health straight from each company's official status page.

`https://ukdata.reliness.co.uk/mcp/service-status`

`github_status`, `discord_status`, `cloudflare_status`, `openai_status`, `atlassian_status`, `shopify_status`, `digitalocean_status`, `slack_status`, `zoom_status`, `anthropic_claude_status`

### Software end-of-life and support dates (endoflife.date) (`software-lifecycle`)

Live release, support and end-of-life dates for about 490 products: programming languages, operating systems, databases, frameworks, cloud services and devices. Answers "is this version still supported" and "what is the latest version" from current data rather than stale memory.

`https://ukdata.reliness.co.uk/mcp/software-lifecycle`

`eol_latest_release`, `eol_unsupported_releases`, `eol_products_by_category`, `eol_products_by_vendor_tag`, `eol_product_search`, `eol_tags`

### Software packages and vulnerabilities (`software-supply-chain`)

Latest versions, deprecation, licences and links for npm, PyPI, crates, Go, Maven, NuGet and RubyGems packages; known vulnerabilities for one package or a whole dependency list (OSV).

`https://ukdata.reliness.co.uk/mcp/software-supply-chain`

`package_info`, `vuln_check`

### NOAA space weather and aurora (`space-weather`)

Live space weather from the US NOAA Space Weather Prediction Center: the geomagnetic Kp index now and for the next 3 days, the aurora chance at any location and a plain-English UK aurora outlook, official alerts and storm scales, solar flares, solar wind, radio flux and the sunspot cycle back to 1749.

`https://ukdata.reliness.co.uk/mcp/space-weather`

`kp_index_now`, `kp_forecast_3day`, `aurora_chance_at_location`, `space_weather_scales`, `space_weather_alerts`, `solar_flares_recent`, `solar_wind_speed`, `solar_flux_10cm`

### Spreadsheets and PDFs (`spreadsheets-pdf`)

Write real .xlsx workbooks from rows (or several sheets), read any spreadsheet or CSV from a URL into JSON, and extract text from PDFs page by page.

`https://ukdata.reliness.co.uk/mcp/spreadsheets-pdf`

`make_xlsx`, `read_spreadsheet`, `pdf_to_text`

### UK government and law (`uk-government-law`)

Legislation search and full text, MPs by name or postcode, petitions, GOV.UK search and page content, food alerts, police neighbourhoods.

`https://ukdata.reliness.co.uk/mcp/uk-government-law`

`legislation_search`, `legislation_text`, `mp_lookup`, `petitions_search`, `govuk_search`, `govuk_page`, `food_alerts`, `police_neighbourhood`

### UK NHS and charities (`uk-health-charities`)

NHS organisations from the ODS directory and Charity Commission register details.

`https://ukdata.reliness.co.uk/mcp/uk-health-charities`

`nhs_organisations`, `charity_lookup`

### National Heritage List for England (listed buildings and monuments) (`uk-heritage`)

England's official register of protected heritage, straight from Historic England: listed buildings with their grades, scheduled monuments, registered parks and gardens, battlefields, protected wrecks and World Heritage Sites. Answer 'is it listed', 'what grade' and 'what is protected near here' with list entry numbers and links to the official record.

`https://ukdata.reliness.co.uk/mcp/uk-heritage`

`listed_building_search`, `listed_building_lookup`, `scheduled_monument_search`, `scheduled_monuments_near`, `historic_park_garden_search`, `battlefield_search`, `protected_wreck_search`

### UK Parliament Select Committees (`uk-parliament-scrutiny`)

Find any Commons, Lords or joint select committee and see who sits on it, what it is investigating, who has given evidence and what it has published, straight from the UK Parliament Committees API.

`https://ukdata.reliness.co.uk/mcp/uk-parliament-scrutiny`

`committee_search`, `committee_evidence_sessions`, `written_question_search`, `written_question_detail`, `unanswered_written_questions`, `written_statement_search`, `oral_questions_upcoming`, `early_day_motions_recent`

### UK product safety (`uk-product-safety`)

Product safety alerts, reports and recalls from the Office for Product Safety and Standards.

`https://ukdata.reliness.co.uk/mcp/uk-product-safety`

`product_recalls`

### UK Road Traffic Statistics (DfT counts) (`uk-roads-traffic`)

Official Great Britain road traffic figures from the Department for Transport: where traffic is counted on each road, vehicles per day by type at a counting point, hour-by-hour survey counts, and annual vehicle miles by council and region. Useful for site selection, planning statements, advertising and area comparisons.

`https://ukdata.reliness.co.uk/mcp/uk-roads-traffic`

`road_traffic_flow_at_point`, `road_traffic_hourly_counts`, `local_authority_traffic_totals`, `region_traffic_by_vehicle_type`, `traffic_local_authority_find`, `traffic_regions_list`

### UK statistics and Bank of England (`uk-statistics-money`)

Search ONS statistics and pull any ONS time series by CDID (inflation, unemployment, GDP), Bank of England series (Bank Rate, exchange rates, mortgage rates), and the FCA register.

`https://ukdata.reliness.co.uk/mcp/uk-statistics-money`

`ons_search`, `ons_timeseries`, `boe_series`, `fca_search`

### UK trade, property and planning (`uk-trade-property-planning`)

Trade Tariff commodity codes and duties, HMRC monthly exchange rates, UK House Price Index by area, planning applications nationwide, CQC care ratings.

`https://ukdata.reliness.co.uk/mcp/uk-trade-property-planning`

`trade_tariff`, `hmrc_exchange_rates`, `house_price_index`, `planning_search`, `cqc_search`, `cqc_location`

### US politics and government records (`us-politics-government`)

Official US government and politics records that people ask assistants to check: presidential actions, Congress votes and membership, Supreme Court status, federal operating status and Treasury figures. Answers come from the official publishers, with dates and links, instead of from stale training data.

`https://ukdata.reliness.co.uk/mcp/us-politics-government`

`executive_order_by_number`, `federal_register_document`, `us_government_operating_status`, `us_shutdown_now`, `opm_status_history`

### Utilities (`utilities`)

Domain registration (RDAP), unshorten URLs, HTTPS checks, QR codes, calendar invites, text statistics, hashes and UUIDs, JSON validation.

`https://ukdata.reliness.co.uk/mcp/utilities`

`rdap_lookup`, `unshorten`, `ssl_check`, `qr_code`, `ical_event`, `text_stats`, `hash_text`, `json_validate`

### Business validation (`validation`)

Check a VAT registration number (UK and EU, official sources) for invoicing, onboarding, KYB and anti-fraud. Returns the registered business name and address where available.

`https://ukdata.reliness.co.uk/mcp/validation`

`vat_check`, `uk_vat_check`

### US Vehicle Safety (NHTSA recalls, complaints, crash ratings, vPIC) (`vehicles-safety`)

Check a car before you buy or drive it: US safety recalls, owner-filed defect complaints, NCAP crash-test star ratings, driver-assist equipment and problem counts, plus model lists, VIN maker codes and registered manufacturer details, all from the US National Highway Traffic Safety Administration (NHTSA). Covers vehicles sold in the US, which includes many models also sold in the UK.

`https://ukdata.reliness.co.uk/mcp/vehicles-safety`

`vehicle_recalls`, `recall_campaign_details`, `vehicle_complaints`, `complaint_by_odi_number`, `vehicle_crash_ratings`, `vehicle_driver_assist_features`, `vehicle_problem_counts`, `vehicle_models_for_make_year`, `wmi_manufacturer_lookup`, `vehicle_manufacturer_details`

### MET Norway forecasts, marine, sun and moon (worldwide) (`weather-forecasts`)

Worldwide point forecasts by job (hour by hour, day by day, rain in the next hours, UV, wind, cloud layers), sea-state and sea temperature forecasts for northern European waters, and sunrise, sunset and moon phase for any place and date. Data from the Norwegian Meteorological Institute (MET Norway), returned in plain units with plain-English conditions.

`https://ukdata.reliness.co.uk/mcp/weather-forecasts`

`rain_forecast_next_hours`, `uv_index_forecast`, `wind_forecast`, `cloud_cover_forecast`, `marine_forecast`, `sea_temperature`, `sunrise_sunset`, `moon_phase`

### Weather observations: airport METAR readings, TAF forecasts and aviation hazards (`weather-observations`)

Official, station-exact weather observations and aviation forecasts from the NOAA/NWS Aviation Weather Center: the readings that city temperature contracts, pilots and travellers rely on, as opposed to modelled forecasts. Current and past airport reports, a station's daily high and low, terminal forecasts, pilot reports and US hazard warnings.

`https://ukdata.reliness.co.uk/mcp/weather-observations`

`metar_latest`, `metar_history`, `taf_forecast`, `pireps_near_airport`

### Weather and places (`weather-places`)

Weather now and up to 9 days ahead anywhere (MET Norway), and Great Britain place-name lookup.

`https://ukdata.reliness.co.uk/mcp/weather-places`

`geocode`, `weather`

### Web reader (`web-reader`)

Fetch a page and get clean markdown or text, title, description and links. No scraping infrastructure to run.

`https://ukdata.reliness.co.uk/mcp/web-reader`

`read_url`

### Web research (`web-research`)

Wayback Machine snapshots of any URL, on-page SEO audits, and Wikidata facts about companies, people and places.

`https://ukdata.reliness.co.uk/mcp/web-research`

`wayback`, `seo_audit`, `wikidata_lookup`


## Data and licences

Data comes from its official publishers (Companies House, HM Land Registry, DLUHC EPC register, Find a Tender, Contracts Finder, the Bank of England, ONS, UK Parliament, FCDO, DVSA, Environment Agency, Defra, OFSI, OFAC, the EU and UN sanctions lists, and others), used under their open licences. Each response names its source.

## Support

ben@reliness.co.uk · https://reliness.co.uk · Reliness Ltd, London
