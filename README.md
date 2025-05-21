# Preppin Data 2023 Week 2
This is a challenge from [Summer of SQL](https://github.com/wjsutton/the_summer_of_sql) to help gain skills and confidence in SQL.

Skills tested in challenge 3.2:
- String manipulation with REPLACE


## Challenge: Preppin Data 2023 Week 2

Inputs
- A list of the transactions, with information about the receiving bank account

![Input](https://blogger.googleusercontent.com/img/a/AVvXsEiAItr9blizuA4ej88cecGYqGdUDrReg6X245S-3nwVcwCEdQJTT_Zgq3LaqRPNp3Yk1wDKBarJ2rV-77rWIxmkB9n_d6IH6SniOe-zfAoO0u1iF7_ClvnK_OXoD_yXoshxbhhd633mzwtrYFaTHJu-GbrrBkUeF-meGbHvtIV7wUemkRK-5xO7Djk1qg).

- A lookup table for the SWIFT Bank Codes

![Input](https://blogger.googleusercontent.com/img/a/AVvXsEg6fOt52HxeinlLBH6vvkEe80nUpprIXfLmE4H7qwt0U4BNU9n4fzzw-_5bWOI77WJCAId9YFK6Ezzt05F8md6OtyVqeWulnhfukFe1tsv39cQtTU1w952ykX8yb2yOLQp8yyl9ojoj_OHS5vuh6qh61cdI33ZD4ARegghcajZSkj37pErkpnCU_nSHKw). 

Data Source Bank has a requirement to construct International Bank Account Numbers (IBANs), even for Transactions taking place in the UK. We have all the information in separate fields, we just need to put it altogether in the following order:

![Input](https://blogger.googleusercontent.com/img/a/AVvXsEg6cHU6JOCWWyUbCGBixif-Cj3CvRJNRr3RFzcpG7kI8zzL3eAWKBZPdu2UVqivMHILO-zaT2bJ9F2iaNfVWgZIAro_IOwwKi-GjJFVQyJ_O9iE-0X7Iin4vZxbqHiuEsPQp2nDtIjAARQ_aCrSbnmJU6LiU7L64P3gzS68jU9b7_ScOnYI3LOciKGwUw). 

Requirements:
- In the Transactions table, there is a Sort Code field which contains dashes. We need to remove these so just have a 6 digit string
- Use the SWIFT Bank Code lookup table to bring in additional information about the SWIFT code and Check Digits of the receiving bank account
- Add a field for the Country. All these transactions take place in the UK so the Country Code should be GB
- Create the IBAN as above watch out for trying to combine sting fields with numeric fields - check data types
- Remove unnecessary fields


## Output
````sql
SELECT 
transaction_id,
'GB' || check_digits || swift_code || REPLACE(sort_code,'-','') || account_number as iban
FROM pd2023_wk02_transactions as t
INNER JOIN pd2023_wk02_swift_codes as s on t.bank = s.bank
````
| TRANSACTION_ID | IBAN                    |
|----------------|-------------------------|
| 3888           | GB12DSBX95988262230725  |
| 7423           | GB22HLFX49312675616805  |
| 3286           | GB22HLFX21853047326725  |
| 6764           | GB12DSBX29723910570182  |
| 2021           | GBC1LOYD59175172261023  |
| 9373           | GB4BHBUK24151244568613  |
| 7983           | GB2LNWBK67189758775796  |
| 8813           | GBC1LOYD63589183475180  |
| 3270           | GB2LNWBK16710742126094  |
| 2868           | GB4BHBUK81899653579089  |
| 9195           | GB22BARC29369996432979  |
| 2797           | GB22HLFX36632147474979  |
| 9096           | GB4BHBUK74259532710603  |
| 7485           | GBC1LOYD63461763007765  |
| 2340           | GB4BHBUK95741982753835  |
