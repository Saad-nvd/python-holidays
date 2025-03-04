========
holidays
========

A fast, efficient Python library for generating country- and subdivision- (e.g.
state or province) specific sets of government-designated holidays on the fly.
It aims to make determining whether a specific date is a holiday as fast and
flexible as possible.

.. |downloads| image:: https://img.shields.io/pypi/dm/holidays?color=41B5BE&style=flat
    :target: https://pypi.org/project/holidays
    :alt: PyPI downloads

.. |version| image:: https://img.shields.io/pypi/v/holidays?color=41B5BE&label=version&style=flat
    :target: https://pypi.org/project/holidays
    :alt: PyPI version

.. |release date| image:: https://img.shields.io/github/release-date/vacanza/python-holidays?color=41B5BE&style=flat
    :target: https://github.com/vacanza/python-holidays/releases
    :alt: PyPI release date

.. |status| image:: https://img.shields.io/github/actions/workflow/status/vacanza/python-holidays/ci-cd.yml?branch=dev&color=41BE4A&style=flat
    :target: https://github.com/vacanza/python-holidays/actions/workflows/ci-cd.yml?query=branch%3Adev
    :alt: CI/CD status

.. |documentation| image:: https://img.shields.io/readthedocs/python-holidays?color=41BE4A&style=flat
    :target: https://python-holidays.readthedocs.io/en/latest/?badge=latest
    :alt: Documentation status

.. |license| image:: https://img.shields.io/github/license/vacanza/python-holidays?color=41B5BE&style=flat
    :target: https://github.com/vacanza/python-holidays/blob/dev/LICENSE
    :alt: License

.. |python versions| image:: https://img.shields.io/pypi/pyversions/holidays?label=python&color=41B5BE&style=flat
    :target: https://pypi.org/project/holidays
    :alt: Python supported versions

.. |style| image:: https://img.shields.io/badge/style-ruff-41B5BE?style=flat
    :target: https://github.com/astral-sh/ruff
    :alt: Code style

.. |coverage| image:: https://img.shields.io/codecov/c/github/vacanza/python-holidays/dev?color=41B5BE&style=flat
    :target: https://app.codecov.io/gh/vacanza/python-holidays
    :alt: Code coverage

.. |stars| image:: https://img.shields.io/github/stars/vacanza/python-holidays?color=41BE4A&style=flat
    :target: https://github.com/vacanza/python-holidays/stargazers
    :alt: GitHub stars

.. |forks| image:: https://img.shields.io/github/forks/vacanza/python-holidays?color=41BE4A&style=flat
    :target: https://github.com/vacanza/python-holidays/forks
    :alt: GitHub forks

.. |contributors| image:: https://img.shields.io/github/contributors/vacanza/python-holidays?color=41BE4A&style=flat
    :target: https://github.com/vacanza/python-holidays/graphs/contributors
    :alt: GitHub contributors

.. |last commit| image:: https://img.shields.io/github/last-commit/vacanza/python-holidays/dev?color=41BE4A&style=flat
    :target: https://github.com/vacanza/python-holidays/commits/dev
    :alt: GitHub last commit

+--------+------------------------------------------------+
| PyPI   | |downloads| |version| |release date|           |
+--------+------------------------------------------------+
| CI/CD  | |status| |documentation|                       |
+--------+------------------------------------------------+
| Code   | |license| |python versions| |style| |coverage| |
+--------+------------------------------------------------+
| GitHub | |stars| |forks| |contributors| |last commit|   |
+--------+------------------------------------------------+

Install
-------

The latest stable version can always be installed or updated via pip:

.. code-block:: shell

    $ pip install --upgrade holidays

The latest development (dev) version can be installed directly from GitHub:

.. code-block:: shell

    $ pip install --upgrade https://github.com/vacanza/python-holidays/tarball/dev

All new features are always first pushed to dev branch, then released on
main branch upon official version upgrades.

Documentation
-------------

.. _Read the Docs: https://python-holidays.readthedocs.io/

The documentation is hosted on `Read the Docs`_.


Quick Start
-----------

.. code-block:: python

    from datetime import date
    import holidays

    us_holidays = holidays.US()  # this is a dict-like object
    # the below is the same, but takes a string:
    us_holidays = holidays.country_holidays('US')  # this is a dict-like object

    nyse_holidays = holidays.NYSE()  # this is a dict-like object
    # the below is the same, but takes a string:
    nyse_holidays = holidays.financial_holidays('NYSE')  # this is a dict-like object

    date(2015, 1, 1) in us_holidays  # True
    date(2015, 1, 2) in us_holidays  # False
    us_holidays.get('2014-01-01')  # "New Year's Day"

The HolidayBase dict-like class will also recognize date strings and Unix
timestamps:

.. code-block:: python

    '2014-01-01' in us_holidays  # True
    '1/1/2014' in us_holidays    # True
    1388597445 in us_holidays    # True

Some holidays may be only present in parts of a country:

.. code-block:: python

    us_pr_holidays = holidays.country_holidays('US', subdiv='PR')
    '2018-01-06' in us_holidays     # False
    '2018-01-06' in us_pr_holidays  # True

.. _python-holidays documentation: https://python-holidays.readthedocs.io/

Please see the `python-holidays documentation`_ for additional examples and
detailed information.


Available Countries
-------------------

.. _ISO 3166-1 alpha-2 code: https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes
.. _ISO 3166-2 code: https://en.wikipedia.org/wiki/ISO_3166-2
.. _ISO 639-1 code: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
.. _ISO 639-2 code: https://en.wikipedia.org/wiki/List_of_ISO_639-2_codes

We currently support 148 country codes. The standard way to refer to a country
is by using its `ISO 3166-1 alpha-2 code`_, the same used for domain names, and
for a subdivision its `ISO 3166-2 code`_. Some countries have common or foreign
names or abbreviations as aliases for their subdivisions. These are defined in
the (optional) ``subdivisions_aliases`` attribute.
Some of the countries support more than one language for holiday names output.
A default language is defined by ``default_language`` (optional) attribute
for each entity and is used as a fallback when neither user specified
language nor user locale language available. The default language code is
a `ISO 639-1 code`_. A list of all languages supported by country is defined by
``supported_languages`` (optional) attribute. If there is no designated
`ISO 639-1 code`_ then `ISO 639-2 code`_ can be used.

Many countries have other categories of holidays in addition to common (national-wide) holidays:
bank holidays, school holidays, additional (paid or non-paid) holidays, holidays of state or
public employees, religious holidays (valid only for these religions followers). A list of all
categories supported by country is defined by ``supported_categories`` (optional) attribute.

The following is a list of supported countries, their subdivisions followed by their
aliases (if any) in brackets, available languages and additional holiday categories.
All countries support **PUBLIC** holidays category by default.
All other default values are highlighted with bold:


.. list-table::
   :widths: 20 4 46 20 10
   :header-rows: 1
   :class: tight-table

   * - Country
     - Code
     - Subdivisions
     - Supported Languages
     - Supported Categories
   * - Albania
     - AL
     -
     -
     -
   * - Algeria
     - DZ
     -
     - **ar**, en_US, fr
     -
   * - American Samoa
     - AS
     - Can also be loaded as country US, subdivision AS
     -
     - UNOFFICIAL
   * - Andorra
     - AD
     - Parishes: 02, 03, 04, 05, 06, 07, 08
     -
     -
   * - Angola
     - AO
     -
     - en_US, **pt_AO**, uk
     -
   * - Argentina
     - AR
     -
     - en_US, **es**, uk
     -
   * - Armenia
     - AM
     -
     - en_US, **hy**
     -
   * - Aruba
     - AW
     -
     - en_US, nl, **pap_AW**, uk
     -
   * - Australia
     - AU
     - States and territories: ACT (Australian Capital Territory), NSW (New South Wales), NT (Northern Territory), QLD (Queensland), SA (South Australia), TAS (Tasmania), VIC (Victoria), WA (Western Australia)
     -
     - BANK, HALF_DAY
   * - Austria
     - AT
     - States: 1 (Burgenland, Bgld, B), 2 (Kärnten, Ktn, K), 3 (Niederösterreich, NÖ, N), 4 (Oberösterreich, OÖ, O), 5 (Salzburg, Sbg, S), 6 (Steiermark, Stmk, St), 7 (Tirol, T), 8 (Vorarlberg, Vbg, V), 9 (Wien, W)
     - **de**, en_US, uk
     - BANK
   * - Azerbaijan
     - AZ
     -
     - **az**, en_US, uk
     - WORKDAY
   * - Bahamas
     - BS
     -
     -
     -
   * - Bahrain
     - BH
     -
     - **ar**, en_US
     -
   * - Bangladesh
     - BD
     -
     -
     -
   * - Barbados
     - BB
     -
     -
     -
   * - Belarus
     - BY
     -
     - **be**, en_US
     -
   * - Belgium
     - BE
     -
     - de, en_US, fr, **nl**, uk
     - BANK
   * - Belize
     - BZ
     -
     -
     -
   * - Bolivia
     - BO
     - Departments: B, C, H, L, N, O, P, S, T
     - en_US, **es**, uk
     -
   * - Bosnia and Herzegovina
     - BA
     - Entities and district: BIH, BRC, SRP
     - **bs**, en_US, sr, uk
     -
   * - Botswana
     - BW
     -
     -
     -
   * - Brazil
     - BR
     - States: AC, AL, AM, AP, BA, CE, DF, ES, GO, MA, MG, MS, MT, PA, PB, PE, PI, PR, RJ, RN, RO, RR, RS, SC, SE, SP, TO
     -
     - OPTIONAL
   * - Brunei
     - BN
     -
     - en_US, **ms**, th
     -
   * - Bulgaria
     - BG
     -
     - **bg**, en_US, uk
     - SCHOOL
   * - Burkina Faso
     - BF
     -
     -
     -
   * - Burundi
     - BI
     -
     -
     -
   * - Cambodia
     - KH
     -
     - en_US, **km**, th
     -
   * - Cameroon
     - CM
     -
     -
     -
   * - Canada
     - CA
     - Provinces and territories: AB, BC, MB, NB, NL, NS, NT, NU, ON, PE, QC, SK, YT
     - ar, **en_CA**, en_US, fr, th
     - GOVERNMENT, OPTIONAL
   * - Chad
     - TD
     -
     -
     -
   * - Chile
     - CL
     - Regions: AI, AN, AP, AR, AT, BI, CO, LI, LL, LR, MA, ML, NB, RM, TA, VS
     - en_US, **es**, uk
     - BANK
   * - China
     - CN
     -
     - en_US, th, **zh_CN**, zh_TW
     - HALF_DAY
   * - Colombia
     - CO
     -
     - en_US, **es**, uk
     -
   * - Costa Rica
     - CR
     -
     - en_US, **es**, uk
     - OPTIONAL
   * - Croatia
     - HR
     -
     - en_US, **hr**, uk
     -
   * - Cuba
     - CU
     -
     - en_US, **es**, uk
     -
   * - Curacao
     - CW
     -
     - en_US, nl, **pap_CW**, uk
     -
   * - Cyprus
     - CY
     -
     - **el**, en_CY, en_US, uk
     - BANK, OPTIONAL
   * - Czechia
     - CZ
     -
     - **cs**, en_US, sk, uk
     -
   * - Denmark
     - DK
     -
     - **da**, en_US, uk
     - OPTIONAL
   * - Djibouti
     - DJ
     -
     - ar, en_US, **fr**
     -
   * - Dominican Republic
     - DO
     -
     - en_US, **es**, uk
     -
   * - Ecuador
     - EC
     -
     - en_US, **es**, uk
     -
   * - Egypt
     - EG
     -
     - **ar**, en_US
     -
   * - El Salvador
     - SV
     - Departments: AH, CA, CH, CU, LI, MO, PA, SA, SM, SO, SS, SV, UN, US
     -
     -
   * - Estonia
     - EE
     -
     - en_US, **et**, uk
     -
   * - Eswatini
     - SZ
     -
     -
     -
   * - Ethiopia
     - ET
     -
     - **am**, ar, en_US
     -
   * - Finland
     - FI
     -
     - en_US, **fi**, sv, uk
     -
   * - France
     - FR
     - Départements: BL, GES, GP, GY, MF, MQ, NC, PF, RE, WF, YT
     - en_US, **fr**, uk
     -
   * - Gabon
     - GA
     -
     -
     -
   * - Georgia
     - GE
     -
     - en_US, **ka**, uk
     - GOVERNMENT
   * - Germany
     - DE
     - States: BB, BE, BW, BY, BYP, HB, HE, HH, MV, NI, NW, RP, SH, SL, SN, ST, TH
     - **de**, en_US, uk
     -
   * - Ghana
     - GH
     -
     -
     -
   * - Greece
     - GR
     -
     - **el**, en_US, uk
     - HALF_DAY
   * - Greenland
     - GL
     -
     - da, en_US, **kl**
     - OPTIONAL
   * - Guam
     - GU
     - Can also be loaded as country US, subdivision GU
     -
     - UNOFFICIAL
   * - Guatemala
     - GT
     -
     - en_US, **es**
     -
   * - Honduras
     - HN
     -
     - en_US, **es**, uk
     -
   * - Hong Kong
     - HK
     -
     -
     - OPTIONAL
   * - Hungary
     - HU
     -
     - en_US, **hu**, uk
     -
   * - Iceland
     - IS
     -
     - en_US, **is**, uk
     -
   * - India
     - IN
     - States: AN, AP, AR, AS, BR, CG, CH, DH, DL, GA, GJ, HP, HR, JH, JK, KA, KL, LA, LD, MH, ML, MN, MP, MZ, NL, OD, PB, PY, RJ, SK, TN, TR, TS, UK, UP, WB
     -
     -
   * - Indonesia
     - ID
     -
     - en_US, **id**, uk
     - GOVERNMENT
   * - Iran
     - IR
     -
     - en_US, **fa**
     -
   * - Ireland
     - IE
     -
     -
     -
   * - Isle of Man
     - IM
     -
     -
     -
   * - Israel
     - IL
     -
     - en_US, **he**, uk
     - OPTIONAL, SCHOOL
   * - Italy
     - IT
     - Provinces: AG, AL, AN, AO, AP, AQ, AR, AT, AV, BA, BG, BI, BL, BN, BO, BR, BS, BT, BZ, CA, CB, CE, CH, CL, CN, CO, CR, CS, CT, CZ, EN, FC, FE, FG, FI, FM, FR, GE, GO, GR, IM, IS, KR, LC, LE, LI, LO, LT, LU, MB, MC, ME, MI, MN, MO, MS, MT, NA, NO, NU, OR, PA, PC, PD, PE, PG, PI, PN, PO, PR, PT, PU, PV, PZ, RA, RC, RE, RG, RI, RM, RN, RO, SA, SI, SO, SP, SR, SS, SU, SV, TA, TE, TN, TO, TP, TR, TS, TV, UD, VA, VB, VC, VE, VI, VR, VT, VV. Cities: Andria, Barletta, Cesena, Forli, Pesaro, Trani, Urbino
     -
     -
   * - Jamaica
     - JM
     -
     -
     -
   * - Japan
     - JP
     -
     - en_US, **ja**, th
     - BANK
   * - Jersey
     - JE
     -
     -
     -
   * - Jordan
     - JO
     -
     - **ar**, en_US
     -
   * - Kazakhstan
     - KZ
     -
     -
     -
   * - Kenya
     - KE
     -
     -
     -
   * - Kuwait
     - KW
     -
     - **ar**, en_US
     -
   * - Kyrgyzstan
     - KG
     -
     -
     -
   * - Laos
     - LA
     -
     - en_US, **lo**, th
     - BANK, SCHOOL, WORKDAY
   * - Latvia
     - LV
     -
     - en_US, **lv**, uk
     -
   * - Lesotho
     - LS
     -
     -
     -
   * - Liechtenstein
     - LI
     -
     - **de**, en_US, uk
     - BANK
   * - Lithuania
     - LT
     -
     - en_US, **lt**, uk
     -
   * - Luxembourg
     - LU
     -
     - de, en_US, fr, **lb**, uk
     -
   * - Madagascar
     - MG
     -
     - en_US, **mg**, uk
     -
   * - Malawi
     - MW
     -
     -
     -
   * - Malaysia
     - MY
     - States and federal territories: 01 (Johor), 02 (Kedah), 03 (Kelantan), 04 (Melaka), 05 (Negeri Sembilan), 06 (Pahang), 07 (Pulau Pinang), 08 (Perak), 09 (Perlis), 10 (Selangor), 11 (Terengganu), 12 (Sabah), 13 (Sarawak), 14 (WP Kuala Lumpur), 15 (WP Labuan), 16 (WP Putrajaya)
     - en_US, **ms_MY**
     -
   * - Maldives
     - MV
     -
     -
     -
   * - Malta
     - MT
     -
     - en_US, **mt**
     -
   * - Marshall Islands (the)
     - MH
     -
     -
     -
   * - Mexico
     - MX
     -
     - en_US, **es**, uk
     -
   * - Moldova
     - MD
     -
     - en_US, **ro**, uk
     -
   * - Monaco
     - MC
     -
     - en_US, **fr**, uk
     -
   * - Montenegro
     - ME
     -
     -
     -
   * - Morocco
     - MA
     -
     - **ar**, en_US, fr
     -
   * - Mozambique
     - MZ
     -
     - en_US, **pt_MZ**, uk
     -
   * - Namibia
     - NA
     -
     -
     -
   * - Netherlands
     - NL
     -
     - en_US, **nl**, uk
     - OPTIONAL
   * - New Zealand
     - NZ
     - Regions: AUK, BOP, CAN, CIT, GIS, HKB, MBH, MWT, NSN, NTL, OTA, STL, TAS, TKI, WGN, WKO, WTC
     -
     -
   * - Nicaragua
     - NI
     - Departments: AN, AS, BO, CA, CI, CO, ES, GR, JI, LE, MD, **MN**, MS, MT, NS, RI, SJ
     - en_US, **es**, uk
     -
   * - Nigeria
     - NG
     -
     -
     -
   * - Northern Mariana Islands (the)
     - MP
     - Can also be loaded as country US, subdivision MP
     -
     - UNOFFICIAL
   * - North Macedonia
     - MK
     -
     -
     -
   * - Norway
     - NO
     -
     - en_US, **no**, uk
     -
   * - Pakistan
     - PK
     -
     -
     -
   * - Palau
     - PW
     -
     -
     - ARMED_FORCES, HALF_DAY
   * - Panama
     - PA
     -
     -
     -
   * - Papua New Guinea
     - PG
     -
     -
     -
   * - Paraguay
     - PY
     -
     - en_US, **es**, uk
     - GOVERNMENT
   * - Peru
     - PE
     -
     - en_US, **es**, uk
     -
   * - Philippines
     - PH
     -
     -
     -
   * - Poland
     - PL
     -
     - en_US, **pl**, uk
     -
   * - Portugal
     - PT
     - Districts: 01, 02, 03, 04, 05, 06, 07, 08, 09, 10, 11, 12, 13, 14, 15, 16, 17, 18, 20, 30
     - en_US, **pt_PT**, uk
     - OPTIONAL
   * - Puerto Rico
     - PR
     - Can also be loaded as country US, subdivision PR
     -
     - UNOFFICIAL
   * - Romania
     - RO
     -
     - en_US, **ro**, uk
     -
   * - Russia
     - RU
     -
     - en_US, **ru**
     -
   * - San Marino
     - SM
     -
     -
     -
   * - Saudi Arabia
     - SA
     -
     - **ar**, en_US
     -
   * - Serbia
     - RS
     -
     - en_US, **sr**
     -
   * - Seychelles
     - SC
     -
     - **en_SC**, en_US
     -
   * - Singapore
     - SG
     -
     -
     -
   * - Slovakia
     - SK
     -
     - en_US, **sk**, uk
     - WORKDAY
   * - Slovenia
     - SI
     -
     - en_US, **sl**, uk
     -
   * - South Africa
     - ZA
     -
     -
     -
   * - South Korea
     - KR
     -
     - en_US, **ko**, th
     - BANK
   * - Spain
     - ES
     - Autonomous communities: AN, AR, AS, CB, CE, CL, CM, CN, CT, EX, GA, IB, MC, MD, ML, NC, PV, RI, VC
     - en_US, **es**, uk
     -
   * - Sweden
     - SE
     -
     - en_US, **sv**, uk
     -
   * - Switzerland
     - CH
     - Cantons: AG, AI, AR, BL, BS, BE, FR, GE, GL, GR, JU, LU, NE, NW, OW, SG, SH, SZ, SO, TG, TI, UR, VD, VS, ZG, ZH
     - **de**, en_US, fr, it, uk
     - HALF_DAY, OPTIONAL
   * - Taiwan
     - TW
     -
     - en_US, th, zh_CN, **zh_TW**
     -
   * - Tanzania
     - TZ
     -
     - en_US, **sw**
     - BANK
   * - Thailand
     - TH
     -
     - en_US, **th**
     - ARMED_FORCES, BANK, GOVERNMENT, SCHOOL, WORKDAY
   * - Timor Leste
     - TL
     -
     - en_US, **pt_TL**, tet
     - GOVERNMENT, WORKDAY
   * - Tonga
     - TO
     -
     - en_US, **to**
     -
   * - Tunisia
     - TN
     -
     - **ar**, en_US
     -
   * - Turkey
     - TR
     -
     - en_US, **tr**, uk
     - HALF_DAY
   * - Ukraine
     - UA
     -
     - ar, en_US, **uk**
     -
   * - United Arab Emirates
     - AE
     -
     - **ar**, en_US
     -
   * - United Kingdom
     - GB
     - Subdivisions: ENG, NIR, SCT, WLS
     -
     -
   * - United States Minor Outlying Islands
     - UM
     - Can also be loaded as country US, subdivision UM
     -
     - UNOFFICIAL
   * - United States of America (the)
     - US
     - States and territories: AK, AL, AR, AS, AZ, CA, CO, CT, DC, DE, FL, GA, GU, HI, IA, ID, IL, IN, KS, KY, LA, MA, MD, ME, MI, MN, MO, MP, MS, MT, NC, ND, NE, NH, NJ, NM, NV, NY, OH, OK, OR, PA, PR, RI, SC, SD, TN, TX, UM, UT, VA, VI, VT, WA, WI, WV, WY
     -
     - UNOFFICIAL
   * - United States Virgin Islands (the)
     -
     - See Virgin Islands (U.S.)
     -
     - UNOFFICIAL
   * - Uruguay
     - UY
     -
     - en_US, **es**, uk
     - BANK
   * - Uzbekistan
     - UZ
     -
     - en_US, uk, **uz**
     -
   * - Vanuatu
     - VU
     -
     -
     -
   * - Vatican City
     - VA
     -
     -
     -
   * - Venezuela
     - VE
     -
     - en_US, **es**, uk
     -
   * - Vietnam
     - VN
     -
     -
     -
   * - Virgin Islands (U.S.)
     - VI
     - Can also be loaded as country US, subdivision VI
     -
     - UNOFFICIAL
   * - Zambia
     - ZM
     -
     -
     -
   * - Zimbabwe
     - ZW
     -
     -
     -


Available Financial Markets
===========================

.. _ISO 10383 MIC: https://www.iso20022.org/market-identifier-codes

The standard way to refer to a financial market is to use its `ISO 10383 MIC`_
(Market Identifier Code) as a "country" code when available. The
following financial markets are available:

.. list-table::
   :widths: 23 4 83
   :header-rows: 1
   :class: tight-table

   * - Entity
     - Code
     - Info
   * - European Central Bank
     - ECB
     - Trans-European Automated Real-time Gross Settlement (TARGET2)
   * - ICE Futures Europe 
     - IFEU
     - A London-based Investment Exchange holidays
   * - New York Stock Exchange
     - XNYS
     - NYSE market holidays (used by all other US-exchanges, including NASDAQ, etc.)


Contributions
-------------

.. _Issues: https://github.com/vacanza/python-holidays/issues
.. _pull requests: https://github.com/vacanza/python-holidays/pulls
.. _here: https://github.com/vacanza/python-holidays/blob/dev/CONTRIBUTING.rst

Issues_ and `pull requests`_ are always welcome.  Please see
`here`_ for more information.

License
-------

.. __: https://github.com/vacanza/python-holidays/blob/dev/LICENSE

Code and documentation are available according to the MIT License
(see LICENSE__).
