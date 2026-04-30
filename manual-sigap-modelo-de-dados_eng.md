---
country: Brazil
document_name: SIGAP MANUAL V.1
source_file: manual-sigap-modelo-de-dados_eng.pdf
extracted_date: 2026-04-30
jurisdiction: Brazil
---

# SIGAP MANUAL

## V.1

## Version Control

| Version | Date | Observation |
|---|---|---|
| V1 | 06/08/2024 | First version of the Manual |

## Index

- Introduction .................................................................................................................................. 4
- Bet Management System - SIGAP ................................................................................................. 5
  - On data submission ................................................................................................................... 5
  - On data format .......................................................................................................................... 5
  - On submission frequency .......................................................................................................... 7
  - On file processing ...................................................................................................................... 8
- Annex I – Bettor ............................................................................................................................ 9
- Annex II – Wallet ......................................................................................................................... 23
- Annex III – Daily Operator ........................................................................................................... 33
- Annex IV – Monthly Operator ..................................................................................................... 38
- Annex V – Sports Betting............................................................................................................. 49
- Annex VI – Online Games Betting ............................................................................................... 62
- Annex VII – Sports Table ............................................................................................................. 71

## Introduction

This document provides technical information about the Bet Management System - SIGAP module to receive the data submitted by the betting operator agents to the Secretariat of Prizes and Bets of the Ministry of Finance, as established on art. 10 of Ordinance SPA/MF No. 722, of 02 of May of 2024.

The betting operator agents must observe the data model and integration requirements on this Manual.

As per the single paragraph of art. 10 of the Ordinance aforementioned, the Secretariat of Prizes and Bets of the Ministry of Finance may, at any given time, request the betting operator agent for further information not provided on this Manual.

## Bet Management System - SIGAP

The Bet Management System - SIGAP enables legal persons who are interested in possessing a licence to explore fixed odds betting lottery modality within the nation to submit the corresponding requirements, and enables betting operator agents to send the data regarding their operations to the Secretariat of Prizes and Bets.

This system is available online, it uses internet as the means of communication and requires appropriate resources to grant data security to what is received from the betting operator agents.

### On data submission

To submit the data provided on this Manual to SIGAP, the betting operator agents must:

1. implement submission systems integration with API (Application Programming Interface) REST (Representational State Transfer), made available by the Secretariat of Prizes and Bets of the Ministry of Finance, in compliance with TLS protocol (Transport Layer Security) version 1.2, through mutual authentication certificate;
2. digitally sign the files with e-CNPJ digital certification issued by Autoridade Certificadora ICP-Brasil (ICP Certification Authority - Brazil), type A1 or A3 (the digital certificate used must refer to the CNPJ of the legal person authorised by the Secretariat of Prizes and Bets to explore fixed odds betting lottery modality; otherwise, the file will not be received);
3. obtain a temporary access token (Bearer), with an expiration time (whenever said token is expired, the API requests will have their access denied through a returned error, and the betting operator agent will have to request a new token);
4. use API with JSON language (JavaScript Object Notation) as message exchange mechanism, following a simple logical standard that is easily understood by developers, and may be quickly interpreted by the applications; and
5. comply with Gzip (GNU zip) file compression standard with base64binary representation.

Technical and specific information of API usage for the betting operator agents, as well as the expiration time of the temporary tokens, authentication endpoints and file specificities will be available on the web Manual by Serpro.

### On data format

Betting operator agents must observe the following requirements related to data format to be sent to SIGAP:

1. data must be in XML language (Extensible Markup Language) and observe the corresponding XML Schemas defined by the Secretariat of Prizes and Bets, available on https://www.gov.br/fazenda/pt-br/composicao/orgaos/secretaria-de-premios-e-apostas .
2. each file must have 7,500 (seven thousand five hundred) entries maximum. For example, a betting file may have up to 7,500 bets on record, each of them with its corresponding details. A wallet file may contain up to 7,500 bettors wallets per file, with the corresponding details of financial transactions. In other words, “entry” does not equal to each field, or tag, of the XML file, but to the most extensive field (or tag/tuple), such as bets, wallets and bettors.
3. each file must be of up to 3 (three) megabytes, aiming at achieving the highest efficiency of the process.
4. files with different but related information must be coherent. For example, we can imagine a bets batch “Lote001_apostas” (Batch001_bets), which contains 7,500 (seven thousand five hundred) bets. To ensure information reliability and coherence, the betting operator agent must send one or more wallet batches with the financial movements occurred during the period, derived from the bets indicated on “Lote001_apostas”. This idea applies to the other files.
5. the data detailed about the operation must be submitted on six types of files:
   - Bettor, which contains the registration data of each bettor registered on the betting operator agent’s system;
   - Wallet, which contains the record of each financial movement of each bettor during the day;
   - Operator – daily, which contains the additional of the daily operation of the operator agent;
   - Operator – monthly, which contains monthly legal obligations;
   - Sports Betting, which contains detailed data of every sports bet placed by each bettor during the day;
   - Online games betting, which contains data of the bets placed by bettor on online games during the day;
6. different files must be submitted by each brand that explores fixed odds betting of the operator agent (in case an operator agent explores said lottery modality through three brands, each of them must submit the files catalogued on item 4 above to the Secretariat of Prizes and Bets, through SIGAP, except “Operator – daily” and “Operator – monthly” files, for which only one must be submitted per operator agent, as per Table 1).

**Table 1**

| Type of file | Type of submission |
|---|---|
| Bettor | Submission by brand |
| Wallet | Submission by brand |
| Operator – daily | Submission by operator agent |
| Operator – Monthly | Submission by operator agent |
| Sports Betting | Submission by brand |
| Online games betting | Submission by brand |

The data models by type of file are on the annexes of this Manual.

It is important to highlight that the data to be submitted by the betting operator agents to SIGAP must be stored in data centres located in Brazilian territory; or alternatively, out of the national territory in compliance with the requirements on art. 4, §1 of Ordinance No. 722 (2024). In this last case, to comply with the provisions on art. 4, §1, item III, of said Ordinance, data updates must occur at least every 24 hours, with integrity and match testing at least every 7 days.

### On submission frequency

The operator agents must submit the files through SIGAP observing the following frequencies:

**Table 2**

| File | Frequency |
|---|---|
| Bettor | Daily |
| Wallet | Daily |
| Operator – Daily | Daily |
| Operator – Monthly | Monthly |
| Sports Betting | Daily |
| Online games betting | Daily |

The files must be submitted before 06h00 of the day immediately after the referenced day. Thus, for example, the data referring to the bettor file of 10/03/202X must be submitted to SIGAP until 06:00 of 11/03/202X.

It is hereby outlined that the operator agent may submit the files during the referenced day, and thus avoid traffic buildup consequence of sending all the files in a small time frame. In the case of the example above, the operator agent may send the files that are ready to be sent during 10/03/202X, with no necessity to wait until 11/03/202X to send them.

As a reference, the time to be considered as a trading day is from 00h00 to 23h59m59, of Brasília Time Zone (UTC-3).

Files may be rectified after sending them in case of errors in the generation of the original file sent, as long as the requirements observed on the data models of this Manual are met.

### On file processing

Files submitted by the operator agents will undergo two different phases: file structure analysis and data quality analysis. The detailing of each phase of this process is in the online manual of the API, made available by Serpro.

It is important to highlight that the files will only be considered sent by the operator agents after being subjected to both analysis previously referred. In other words, mere submission of the files does not comply with the obligation of data submission as treated on art. 10 of Ordinance SPA/MF No. 722 (2024).

## Annex I – Bettor

### FILE: BETTOR

### SUBMISSION: DAILY

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|

#### HEADER

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Tipo de Arquivo (Type of File) | Indicates whether the file is original or rectifier. There may only be one rectifier Type of File if there is one previous original file already sent and validated. | Numeric (1) | Yes | 1 - Original 2 - Rectifier | 1 tipoArquivo (typeFile) |
| Version | Reference to the XSD file version made available by SPA/MF, basis for file generation. | Text (10) | Yes | This attribute can be found in the root node and contains the XSD version. | 2 versao (version) |
| Date of the movement referred | 1 - In case of an original file, it is the date of the movement, when the betting operator agent’s system implemented the registration, whether they are new or updates on the bettor’s registration. 2 - In case of a rectifier file, it is the date of the movement referred to in the original file. | Date (YYYY-MM-DD) | Yes | Brasília Time Zone (UTC-3) | 3 dataMovimentoRef (dateMovementRef) |
| Batch Number | 1 - When “Type of file” =1, indicate the batch number to be submitted by the operator agent. It must be sequential and there cannot be duplicate batches, unless it refers to a rectified batch. Numbers must be reset every day. 2 - When “Type of file” = 2, indicate the original batch number to be rectified, as submitted by the operator agent. | Numeric (5) | Yes | Daily uninterrupted sequence, there must be as many as daily files to be submitted from the Bettor’s file. | 4 numeroLote (numberBatch) |
| CNPJ | Identification of the National Registry of Legal Persons (CNPJ) of the operator agent, numbers only, including the verification digit. | Numeric (14) | Yes | CNPJ registered in the Federal Revenue Secretariat, numbers only. | 5 CNPJ |
| Brand | Identification of the brand that is exploring the operation, as is in the SPA/MF authorisation. | Text (100) | Yes | Brand associated to the CNPJ authorised to operate by SPA/MF. | 6 marca (brand) |
| Final batch tag | Identifies if the batch sent is the last “Bettor” type of file to be sent on the day. | Numeric (1) | Yes | 0 - No 1 - Yes | 7 idLoteFinal (idBatchFinal) |
| Date/Time file generation | Date/Time of the generation of the file. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes | Brasília Time Zone (UTC-3) | 8 dataHoraGeracao (dateTimeGeneration) |

#### DETAILS

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Bettor Name | Full name of the bettor | Text (60) | Yes | Full name of the bettor as is on the operator agent’s registration | 1 nomeApostador (nameBettor) |
| CPF | Number of the Registry of Physical Person - CPF of the bettor, as registered in the Federal Revenue Secretariat of Brazil. | Text (11) | Yes | - | 2 CPF |
| Date of Birth | Date of birth of the bettor as is on the ID. as is on the operator agent’s registration | Date (YYYY-MM-DD) | Yes | Date of birth of the bettor | 3 dataNascimento (dateBirth) |
| Date/Time of Account Creation | Date/Time when the bettor’s account was created in the betting operator agent. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes | - | 4 dataHoraCriacaoConta (dateTimeCreationAccount) |
| Date of T&C Acceptance | Date when the acceptance of the terms and conditions of the betting operator agent was signed, whether upon account opening by the bettor or in case of updates on the terms. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes | - | 5 dataHoraAceitacaoTC (dateTimeAcceptanceTC) |
| Bettor Status | Current registration status of the bettor. Upon every alteration, the status must be updated and submitted. | Numeric (2) | Yes | 1 - Active 2 - Cancelled 3 - Suspended 4 - Self Excluded 5 - Verification Pending 6 - Precautionary suspension (compulsive behaviour) 7 - Excluded on the basis of court decision 8 - Registration pending for update and yearly validation 9 - Other | 6 statusApostador (statusBettor) |
| Date/time of the Bettor Status | Date/time of the registration of the current bettor status. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes | - | 7 dataHoraStatus (dateTimeStatus) |
| Gender | Indicates the gender of the bettor. | Numeric (1) | Yes | 1 - Male 2 - Female 3 - Other | 8 genero (gender) |
| Pause Period Setting | “Pause” period is defined by the bettor and is identified in days, within which the bettor cannot place bets, only access the operator agent platform to execute withdrawals of their account. | Numeric (1) | Yes. In case of no pause, fill with 0. | 0 - not set 1 - 1 to 5 days 2 - 6 to 10 days 3 - 11 to 15 days 4 - 16 to 20 days 5 - 21 to 25 days 6 - 26 to 30 days 7 - 31 to 35 days 8 - 36 to 40 days 9 - 40 to 45 days | 9 periodoPausa (periodPause) |
| Date/time of the Pause Period Setting | Date/time when the pause period was set. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes, if “Pause Period Setting” is different from 0. | - | 9.1 dataHoraPeriodoPausa (dateTimePeriodPause) |
| Exclusion Period Setting | “Exclusion” consists of impeding the bettor’s ability to place bets, for a specific period measured in months (3, 6, 12, 24, 36, 48, 60) or permanent exclusion, during which they may only access the betting operator agent’s platform to withdraw account balances. | Numeric (2) | Yes. In case of no exclusion, fill 00. | 00 03 06 12 24 36 48 60 99 - Permanent exclusion | 10 periodoExclusao (periodExclusion) |
| Date/time of the Exclusion Period Setting | Date/time when the exclusion period was set by the bettor. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes, if “Exclusion Period Setting” is different from 00. | - | 10.1 dataHoraPeriodoExclusao (dateTimePeriodExclusion) |
| Exclusion on the basis of Court Decision Period Setting | “Exclusion on the basis of court decision” consists of impeding the bettor’s ability to place bets based on a court decision, for a specific period measured in months (1, 2, 3, 6, 12, 60) or Permanent Exclusion, during which they may only access the betting operator agent’s platform to execute withdrawals from their account balance. | Numeric (2) | Yes | 00 01 02 03 06 12 60 99 - Permanent exclusion | 11 periodoExclusaoJudicial (periodExclusionCourt) |
| Date/time of Exclusion on the basis of Court Decision Period Setting | Date/time when the exclusion on the basis of court decision period was set. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes, if “Exclusion on the basis of Court Decision Period Setting” is different from 00. | - | 11.1 dataHoraPeriodoExclusaoJudicial (dateTimePeriodExclusionCourt) |
| Financial Deposit Limit | Maximum amount in Brazilian Reais that the bettor can possibly deposit, within a period indicated. | Numeric (8,2) | No. | It may be registered based on the settings defined by the bettor. If the bettor has defined a monthly limit only, attribute = 2 will be filled with the amount set, for example. It is not compulsory to send all attributes. It contains the following attributes: 1 - day 2 - month 3 - year | 12 limiteAporte (limitDeposit) |
| Spending Limit | Maximum amount of spending on bets, in Brazilian Reais, that the bettor sets, within a period indicated. | Numeric (8,2) | No. | It may be registered based on the settings defined by the bettor. If the bettor has defined a monthly limit only, attribute = 2 will be filled with the amount set, for example. It is not compulsory to send all attributes. It contains the following attributes: 1 - day 2 - month 3 - year | 13 limiteGasto (limitSpending) |
| Time Limit | Maximum time to stay in the operator agent’s platform, defined by the bettor, during a period indicated. | Time (HH-MM-SS) | No. | It may be registered based on the settings defined by the bettor. If the bettor has defined a monthly limit only, attribute = 2 will be filled with the amount set, for example. It is not compulsory to send all attributes. It contains the following attributes: 1 - day 2 - month 3 - year | 14 limiteTempo (limitTime) |
| Losses Limit | Maximum amount of losses on bets, in Brazilian Reais, that the bettor sets, during a period indicated. | Numeric (8,2) | No. | It may be registered based on the settings defined by the bettor. If the bettor has defined a monthly limit only, attribute = 2 will be filled with the amount set, for example. It is not compulsory to send all attributes. It contains the following attributes: 1 - day 2 - month 3 - year | 15 limitePerda (limitLosses) |
| Data Changes | Indicates if there were data changes during the period of file submission. | Numeric (1) | Yes | 1 - Initial registration 2 - Changed | 16 alteracaoDados (alterationsData) |
| Bettors Total | Total number of bettors, independently from their status. Bettors Total must match with the number of bettors of the previous period, plus the number of new registrations, minus the number of cancelled accounts within the referred period. | Numeric (10) | Yes, if the final batch tag equals 1. | - | 17 qtdTotalApostadores (quantityTotalBettors) |
| Suspended Accounts Total | Total number of bettors whose accounts have been suspended during the period. | Numeric (10) | Yes, if the final batch tag equals 1. | - | 18 totalContasSuspensas (totalAccountsSuspended) |
| Cancelled Accounts Total | Total number of bettors whose accounts have been cancelled during the period. | Numeric (10) | Yes, if the final batch tag equals 1. | - | 19 totalContasCanceladas (totalAccountsCancelled) |
| Total of Self-Excluded Bettors | Total number of bettors who excluded themselves during the period. | Numeric (10) | Yes, if the final batch tag equals 1. | - | 20 totalApostadoresAutoExcluidos (totalBettorsSelfExcluded) |
| Justification of File rectification | In case of a rectifier file, submit the justification for file rectification. The rectified file must be only used in cases of error in the file. | Text (100) | Yes, if “Type of File” equals 2. | - | 21 justificativaRetificacao (justificationRectification) |

#### TRAILER

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Digital Signature | Digital signature of the betting operator agent. | Text | Yes | It is constituted by the digital certificate identification, issuing body of the electronic certificate, name (Standard XML Dsig 1.0) Standard W3C of digital signature. | 22 ds:Signature |

## Annex II – Wallet

### FILE: WALLET

### SUBMISSION: DAILY

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|

#### HEADER

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Tipo de Arquivo (Type of File) | Indicates whether the file is original or rectifier. There may only be one rectifier Type of File if there is one previous original file already sent and validated. | Numeric (1) | Yes | 1 - Original 2 - Rectifier | 1 tipoArquivo (typeFile) |
| Version | Reference to the XSD file version made available by SPA/MF, basis for file generation. | Text (10) | Yes | This attribute can be found in the root node and contains the XSD version. | 2 versao (version) |
| Date of the movement referred | 1 - In case of an original file, it is the date of the movement, when the betting operator agent’s system implemented the registration. 2 - In case of a rectifier file, it is the date of the movement referred to in the original file. | Date (YYYY-MM-DD) | Yes | Brasília Time Zone (UTC-3) | 3 dataMovimentoRef (dateMovementRef) |
| Batch Number | 1 - When “Type of file” =1, indicate the batch number to be submitted by the betting operator agent. It must be sequential and there cannot be duplicate batches, unless it refers to a rectified batch. Numbers must be reset every day. 2 - When “Type of file” =2, indicate the original batch number to be rectified, as submitted by the operator agent. | Numeric (5) | Yes | Daily sequential and uninterrupted, there will be as many as daily files to be submitted from the wallet. | 4 numeroLote (numberBatch) |
| CNPJ | Identification of the National Registry of Legal Persons (CNPJ) of the operator agent, numbers only, including the verification digit. | Numeric (14) | Yes | CNPJ Registered in the Federal Revenue Secretariat, numbers only. | 5 CNPJ |
| Brand | Identification of the brand that is exploring the operation, as is in the SPA/MF authorisation. | Text (100) | Yes | Brand associated to the CNPJ authorised to operate by SPA/MF. | 6 marca (brand) |
| Final batch tag | Identifies if the batch sent is the last “Wallet” type of file to be sent on the day. | Numeric (1) | Yes | 0 - No 1 - Yes | 7 idLoteFinal (idBatchFinal) |
| Date/Time file generation | Date/Time of the generation of the file. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes | Brasília Time Zone (UTC-3) | 8 dataHoraGeracao (dateTimeGeneration) |

#### DETAILS

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| CPF | Number of the Registry of Physical Person - CPF of the bettor, as registered in the Federal Revenue Secretariat of Brazil. | Text (11) | Yes | - | 1 CPF |
| Opening Balance of the day | Initial monetary amount of the day, in Brazilian Reais, that the bettor has in their graphic account in the betting operator agent. | Numeric (8,2) | Yes | - | 2 saldoInicial (balanceInitial) |
| Number of Financial Deposits | Number of financial deposits the bettor executed during the day. | Numeric (3) | Yes | - | 3 qtdAportes (quantityDeposits) |
| Financial Deposit ID | Unique identification of the financial deposit operation. | Text (20) | Yes, if “Amount of Financial Deposits” is different from 0. | An ID will be necessary for each financial deposit in the graphic account of the bettor. | 3.1 idAporte (idDeposit) |
| Financial Deposit Amount | Amount, in Brazilian Reais, that the bettor deposited in their wallet. | Numeric (8,2) | Yes, if “Amount of Financial Deposits” is different from 0. | It will be bound to each financial deposit ID, and will always be a positive figure. | 3.1.1 valorAporte (amountDeposit) |
| Date/time of Financial Deposit | Date and time when the bettor deposited the amount in their wallet. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes, if “Amount of Financial Deposits” is different from 0. | It will be bound to each financial deposit ID. | 3.1.2 dataHoraAporte (dateTimeDeposit) |
| Means of Deposit | Means used by the bettor to make the financial deposit. | Numeric (1) | Yes, if “Amount of Financial Deposits” is different from 0. | 1 - Pix (instant payment method developed by the Bank of Brazil) 2 - Debit Card 3 - Pre-paid Card 4 - TED (Available Electronic Transfer of Brazil) 5 - Book Transfer | 3.1.3 meioAporte (meansDeposit) |
| Number of Financial Withdrawals | Number of financial withdrawals executed during the day by the bettor. | Numeric (3) | Yes | - | 4 qtdRetiradas (quantityWithdrawals) |
| ID of Financial Withdrawal | Identification of the financial withdrawal operation. | Text (20) | Yes, if “Number of Financial Withdrawals” is different from 0. | An ID will be necessary for each financial withdrawal from the graphic account of the bettor. | 4.1 idRetirada (idWithdrawal) |
| Amount of Financial Withdrawal | Amount, in Brazilian Reais, that the bettor withdrew from their wallet. | Numeric (8,2) | Yes, if “Number of Financial Withdrawals” is different from 0. | It will be bound to each financial withdrawal ID, and will always be a positive figure. | 4.1.1 valorRetirada (amountWithdrawal) |
| Date/time of Financial Withdrawal | Date and time when the bettor withdrew the amount from their wallet. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes, if “Number of Financial Withdrawals” is different from 0. | It will be bound to each financial withdrawal ID. | 4.1.2 dataHoraRetirada (dateTimeWithdrawal) |
| Number of Prizes paid | Number of prizes paid by the betting operator agent to the bettor during the period. | Numeric (3) | Yes | - | 5 qtdPremios (quantityPrizes) |
| Prize ID | Unique identification of the prize paid to the bettor. | Text (20) | Yes, if “Number of prizes paid” is different from 0. | An ID will be necessary for each prize paid to the bettor, indicating one of the attributes below. 1 - Sports Bet 2 - Online Game | 5.1 idPremio (idPrize) |
| Bet ID | ID of the Bet, as is in the “Sports Betting” file, which gave origin to the prize that is being paid to the bettor. | Text (20) | Yes, if “Number of prizes paid” is different from 0 and with attribute = 1 - Sports Bet. | It will be bound to each prize paid ID generated from the sports bet. | 5.1.1 idAposta (idBet) |
| Session ID | ID of the Session, as is in the “Online games” file, which gave origin to the prize that is being paid to the bettor. | Text (20) | Yes, if “Number of prizes paid” is different from 0 and with attribute = 2 - Online Game. | It will be bound to each prize paid ID generated from the online game. | 5.1.2 idSessao (idSession) |
| Prize Amount | Amount, in Brazilian Reais, that the bettor received in their wallet. | Numeric (8,2) | Yes, if “Number of prizes paid” is different from 0. | It will be bound to each Prize paid ID. | 5.1.3 valorPremio (amountPrize) |
| Date/time of Prize payment | Date and time when the bettor received the prize in their wallet. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes, if “Number of prizes paid” is different from 0. | It will be bound to each Prize paid ID. | 5.1.4 dataHoraPagamentoPremio (dateTimePaymentPrize) |
| Adjustment Indicator | It indicates if any original transaction has been adjusted in any manner by the operator, such as reversals and additions or reductions due to an erroneous original operation. | Numeric (1) | Yes | 1 - Yes 2 - No | 6 indicadorAjuste (indicatorAdjustment) |
| Adjustment ID | Unique identification of the adjustment executed by the operator in the bettor’s account during the period. | Text (10) | Yes, if “Adjustment Indicator” equals 1. | An ID will be necessary for each adjustment executed by the operator agent. | 6.1 idAjuste (idAdjustment) |
| Type of Transaction | It indicates the type of original transaction that suffered the adjustment. | Numeric (1) | Yes, if “Adjustment Indicator” equals 1. | 1 - Financial Deposit 2 - Financial Withdrawal 3 - Bet 4 - Prize | 6.1.1 tipoTransacao (typeTransaction) |
| Date/time Operation Adjustment | In the event of an adjustment in the bettor’s account, its date/time. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes, if “Adjustment Indicator” equals 1. | - | 6.1.2 dataHoraAjuste (dateTimeAdjustment) |
| Amount of the Operation Adjustment | Amount, in Brazilian Reais, of the adjustment executed in the bettor’s graphic account. | Numeric (8,2) | Yes, if “Adjustment Indicator” equals 1. | This field accepts positive and negative figures. | 6.1.3 valorAjuste (amountAdjustment) |
| Reason for Operation Adjustment | Justification of the adjustment executed by the betting operator agent in the bettor’s graphic account. | Numeric (1) | Yes, if “Adjustment Indicator” equals 1. | 1 - Reversal 2 - Addition due to an erroneous original operation. 3 - Reduction due to an erroneous original operation. 4 - Others | 6.1.4 motivoAjuste (reasonAdjustment) |
| Closing Balance of the day | Amount, in Brazilian Reais, that the bettor has in their wallet at the end of the period. It is the addition of every deposit and prizes to the opening balance and adjustments executed, minus the sum of all the withdrawals, bets placed and adjustments executed. | Numeric (8,2) | Yes | - | 7 saldoFinal (balanceFinal) |
| Total number of Prizes | Total number of prizes paid to all bettors during the period. | Numeric (10) | Yes, if the final batch tag equals 1. | - | 8 qtdTotalPremios (quantityTotalPrizes) |
| Total Amount of Prizes | Total sum, in Brazilian Reais, of the prizes paid to all bettors during the period. | Numeric (12,2) | Yes, if the final batch tag equals 1. | - | 9 valTotalPremios (amountTotalPrizes) |
| Justification of File rectification | In case of a rectifier file, submit the justification for the rectification of the file. The rectified file must be only used in cases of error in the file. | Text (100) | Yes, if “Type of File” equals 2. | - | 10 justificativaRetificacao (justificationRectification) |

#### TRAILER

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Digital Signature | Digital signature of the Operator. | Text | Yes | It is constituted by the digital certificate identification, issuing body of the electronic certificate, name (Standard XML Dsig 1.0) Standard W3C of digital signature. | 11 ds:Signature |

## Annex III – Daily Operator

### FILE: OPERATOR

### SUBMISSION: DAILY

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|

#### HEADER

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Tipo de Arquivo (Type of File) | Indicates whether the file is original or rectifier. There may only be one rectifier Type of File if there is one previous original file already sent and validated. | Numeric (1) | Yes | 1 - Original 2 - Rectifier | 1 tipoArquivo (typeFile) |
| Version | Reference to the XSD file version made available by SPA/MF, basis for file generation. | Text (10) | Yes | This attribute can be found in the root node and contains the XSD version. | 2 versao (version) |
| Date of the movement referred | 1 - In case of an original file, it is the date of the movement, when the betting operator agent’s system implemented the registration, whether they are new or updates on the bettor’s registration. 2 - In case of a rectifier file, it is the date of the movement referred to in the original file. | Date (YYYY-MM-DD) | Yes | Brasília Time Zone (UTC-3) | 3 dataMovimentoRef (dateMovementRef) |
| Batch Number | 1 - When “Type of file” =1, indicate the batch number to be submitted by the betting operator agent. It must be sequential and there cannot be duplicate batches, unless it refers to a rectified batch. Numbers must be reset every day. 2 - When “Type of file” =2, indicate the original batch number to be rectified, as submitted by the operator agent. | Numeric (5) | Yes | Daily uninterrupted sequence, there must be as many as daily files of Operator – Daily to be submitted. | 4 numeroLote (numberBatch) |
| CNPJ | Identification of the National Registry of Legal Persons (CNPJ) of the operator agent, numbers only, including the verification digit. | Numeric (14) | Yes | CNPJ registered in the Federal Revenue Secretariat, numbers only. | 5 CNPJ |
| Date/Time File Generation | Date/Time of the generation of the file. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes | Brasília Time Zone (UTC-3) | 6 dataHoraGeracao (dateTimeGeneration) |

#### DETAILS

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Total Balance of Transactional Accounts | Total added daily balance of the transactional accounts of the operator agent, including eventual amounts invested in public federal securities with daily liquidity. | Numeric (12,2) | Yes | - | 1 saldoTotalContTrans (balanceTotalAccountTransactional) |
| Total Available Financial Balance of Bettors | The available financial balance of each bettor corresponds to the liquid balance of the settled deposits and of the financial withdrawals performed, plus the prizes received that are held in the graphic account, under the terms of § 1 of art. 7 of Ordinance SPA/MF No. 615 (2024), minus the amount of bets placed. | Numeric (12,2) | Yes | - | 2 saldoFinTotalDisp (balanceFinalTotalAvailable) |
| Total Amount of Open Bets | It is the total amount of the bets placed by bettors, not available for new operations, that has not been financially settled by the betting operator agent. | Numeric (12,2) | Yes | - | 3 valorTotalApostasCurso (amountTotalBetsOpen) |
| Justification of File rectification | In case of a rectifier file, submit the justification for file rectification. The rectified file must be only used in cases of error in the file. | Text (100) | Yes, if “Type of File” equals 2. | - | 4 justificativaRetificacao (justificationRectification) |

#### TRAILER

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Digital Signature | Digital signature of the betting operator agent. | Text | Yes | It is constituted by the digital certificate identification, issuing body of the electronic certificate, name (Standard XML Dsig 1.0) Standard W3C of digital signature. | 5 ds:Signature |

## Annex IV – Monthly Operator

### FILE: OPERATOR

### SUBMISSION: MONTHLY

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|

#### HEADER

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Tipo de Arquivo (Type of File) | Indicates whether the file is original or rectifier. There may only be one rectifier Type of File if there is one previous original file already sent and validated. | Numeric (1) | Yes | 1 - Original 2 - Rectifier | 1 tipoArquivo (typeFile) |
| Version | Reference to the XSD file version made available by SPA/MF, basis for file generation. | Text (10) | Yes | This attribute can be found in the root node and contains the XSD version. | 2 versao (version) |
| Date of the movement referred | 1 - In case of an original file, it is the date of the movement, when the betting operator agent’s system implemented the registration. 2 - In case of a rectifier file, it is the date of the movement referred to in the original file. | Date (YYYY-MM-DD) | Yes | Brasília Time Zone (UTC-3) | 3 dataMovimentoRef (dateMovementRef) |
| Batch Number | 1 - When “Type of file” =1, indicate the batch number to be submitted by the operator agent. It must be sequential and there cannot be duplicate batches, unless it refers to a rectified batch. Numbers must be reset every day. 2 - When “Type of file” =2, indicate the original batch number to be rectified, as submitted by the operator agent. | Numeric (5) | Yes | Daily uninterrupted sequence, there must be as many as daily files of Operator – Monthly to be submitted. | 4 numeroLote (numberBatch) |
| CNPJ | Identification of the National Registry of Legal Persons (CNPJ) of the operator agent, numbers only, including the verification digit. | Numeric (14) | Yes | CNPJ registered in the Federal Revenue Secretariat, numbers only. | 5 CNPJ |
| Date/Time file generation | Date/Time of the generation of the file. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes | Brasília Time Zone (UTC-3) | 6 dataHoraGeracao (dateTimeGeneration) |

#### DETAILS

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Social Security Amount Collected | Amount allocated to Social Security - 10% to be collected monthly, as provided by item IV-A, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 1 valSegSocialRecolhido (amountSocialSecurityCollected) |
| Amont Allocated to Education | Amount allocated to the education field - 10%, as provided by item I, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 2 valDestEducacao (amountAllocatedEducation) |
| Amount Allocated to Basic Education Schools | Amount allocated to public basic education schools of state and municipal networks - 6.50%, as provided by line a, item I, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 2.1 valDestEscBasica (amountAllocatedBasicSchool) |
| Amount Allocated to Public Technical High Schools | Amount allocated to public technical high schools of state and municipal networks - 3.50%, as provided by line b, item I, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 2.2 valDestEscTecnica (amountAllocatedTechnicalSchool) |
| Amount Allocated to Public Security | Amount allocated to the public security field - 13.60%, as provided by item I, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 3 valDestSegPublica (amountAllocatedPublicSecurity) |
| Amount Allocated to the National Fund for Public Security - FNSP | Amount allocated to FNSP - 12.60%, as provided by line a, item II, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 3.1 valDestFNSP (amountAllocatedFNSP) |
| Amount Allocated to the Border Control Integrated System - SISFRON | Amount allocated to SISFRON - 1%, as provided by line b, item II, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 3.2 valDestSisfron (amountAllocatedSisfron) |
| Amont Allocated to Sports | Amount allocated to the sports field - 36%, as provided by item III, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 4 valDestEsporte (amountAllocatedSport) |
| Amount Allocated to the entities of the National System of Public Security - SINESP and athletes | Amount allocated to SINESP and athletes’ entities - 7.30%, as provided by line a, item III, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 4.1 valDestSinespAtletas (amountAllocatedSinespAthletes) |
| Amount Allocated to the Brazilian Olympic Committee - COB | Amont Allocated to the COB - 2.20%, as provided by line b, item III, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 4.2 valDestCOB (amountAllocatedCOB) |
| Amount Allocated to the Brazilian Paralympic Committee - CPB | Amount allocated to CPB - 1.30%, as provided by line c, item III, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 4.3 valDestCPB (amountAllocatedCPB) |
| Amount Allocated to the Brazilian Clubs Committee - CBC | Amont allocated to the CBC - 0.70%, as provided by line d, item III, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 4.4 valDestCBC (amountAllocatedCBC) |
| Amont Allocated to the Brazilian Confederation for School Sports - CBDE | Amont allocated to CBDE - 0.50%, as provided by line e, item III, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 4.5 valDestCBDE (amountAllocatedCBDE) |
| Amont Allocated to the Brazilian Confederation for University Sports - CBDU | Amont allocated to CBDU - 0.50%, as provided by line f, item III, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 4.6 valDestCBDU (amountAllocatedCBDU) |
| Amount Allocated to the Brazilian Committee of Paralympic Clubs - CBCP | Amont allocated to the CBCP - 0.30%, as provided by line g, item III, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 4.7 valDestCBCP (amountAllocatedCBCP) |
| Amount Allocated to the Ministry of Sports | Amount allocated to Ministry of Sports - 22.20%, as provided by line h, item III, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 4.8 valDestMinEsporte (amountAllocatedMinSports) |
| Amount Allocated to Sports Offices | Amount allocated to sports offices, or equivalent Federal or State bodies - 0.70%, as provided by line i, item III, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 4.9 valDestSecEsporte (amountAllocatedOfficeSports) |
| Amount Allocated to the Brazilian Committee of Master Sports - CBEM | Amont allocated to the CBEM - 0.30%, as provided by line j, item III, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 4.10 valDestCBEM (amountAllocatedCBEM) |
| Amont Allocated to Tourism | Amount allocated to the tourism field - 28%, as provided by item V, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 5 valDestTurismo (amountAllocatedTourism) |
| Amount Allocated to the Agency for International Promotion of Tourism of Brazil - EMBRATUR | Amount allocated to EMBATUR - 5.60%, as provided by line a, item V, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 5.1 valDestEmbratur (amountAllocatedEmbratur) |
| Amount Allocated to the Ministry of Tourism | Amount allocated to Ministry of Tourism - 22.40%, as provided by line b, item V, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 5.2 valDestMinTurismo (amountAllocatedMinTourism) |
| Amount Allocated to the Ministry of Health | Amount allocated to the Ministry of Health - 1%, as provided by item VI, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 6 valDestSaude (amountAllocatedHealth) |
| Amont Allocated to the National Federation of Associations of Parents and Friends of People with Disabilities - FENAPAES | Amount allocated to FENAPAES - 0.20%, as provided by line a, item VII, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 7 valDestFenapaes (amountAllocatedFenapaes) |
| Amont Allocated to the National Federation of Associations Pestalozzi Fenapestalozzi | Amont allocated to Fenapestalozzi - 0.20%, as provided by line b, item VII, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 8 valDestFenapestalozzi (amountAllocatedFenapestalozzi) |
| Amount Allocated to the Red Cross of Brazil | Amount allocated to the Red Cross of Brazil - 0.10%, as provided by line c, item VII, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 9 valDestCruzVermBrasil (amountAllocatedRedCrossBrazil) |
| Amount Allocated to the Federal Police Equipment and Operations Fund - FUNAPOL | Amont allocated to FUNAPOL - 0.50%, as provided by item VIII, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 10 valDestFunapol (amountAllocatedFUNAPOL) |
| Amount Allocated to the Agency for Industrial Development of Brazil - ABDI | Amont allocated to ABDI - 0.40%, as provided by item IX, §1-A, art. 30 of Law No. 13,756 (2018). | Numeric (12,2) | Yes | - | 11 valDestABDI (amountAllocatedABDI) |
| Amount of Winnings of Prescribed Prizes Collected for FIES | Monthly sum of total amounts of prescribed prizes collected for FIES. | Numeric (12,2) | Yes | - | 12 valFIESGanPresc (amountFIESWinningsPrescribed) |
| Total Amount of GGR Operator | It constitutes the amount of GGR related to every fixed odds bets of the operator agent during the period, including online games bets. It corresponds to the amount of the referred bets minus prizes paid to bettors. | Numeric (12,2) | Yes | - | 13 ggrTotal |
| Inspection Rates Collected | Amount of monthly inspection rates collected through the Federal Collection Guide - GRU. | Numeric (12,2) | Yes | - | 14 taxaFiscRecolhida (rateInspectionCollected) |
| Average Daily Access Time | Average of total time, measured in hours, of daily access of bettors to the betting operator agent system during the referred period. | Numeric (2,2) | Yes | - | 15 mediaAcessoDiario (averageAccessDaily) |
| Justification of File Rectification | In case of a rectifier file, submit the justification for the rectification of the file. The rectified file must be only used in cases of error in the file. | Text (100) | Yes, if “Type of File” equals 2. | - | 16 justificativaRetificacao (justificationRectification) |

#### TRAILER

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Digital Signature | Digital signature of the operator agent. | Text | Yes | It is constituted by the digital certificate identification, issuing body of the electronic certificate, name (Standard XML Dsig 1.0) Standard W3C of digital signature. | 17 ds:Signature |

## Annex V – Sports Betting

### FILE: SPORTS BETTING

### SUBMISSION: DAILY

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|

#### HEADER

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Tipo de Arquivo (Type of File) | Indicates whether the file is original or rectifier. There may only be one rectifier Type of File if there is one previous original file already sent and validated. | Numeric (1) | Yes | 1 - Original 2 - Rectifier | 1 tipoArquivo (typeFile) |
| Version | Reference to the XSD file version made available by SPA/MF, basis for file generation. | Text (10) | Yes | This attribute can be found in the root node and contains the XSD version. | 2 versao (version) |
| Date of the movement referred | 1 - In case of an original file, it is the date of the movement, when the betting operator agent’s system implemented the registration, whether they are new registrations, adjustments to previous releases, results of events such as bets cancellation or suspension, or evolutions of situations related to bets of previous movements, such as the late settlement of a bet. 2 - In case of a rectifier file, it is the date of the movement referred to in the original file. | Date (YYYY-MM-DD) | Yes | Brasília Time Zone (UTC-3) | 3 dataMovimentoRef (dateMovementRef) |
| Batch Number | 1 - When “Type of file” =1, indicate the batch number to be submitted by the operator agent. It must be sequential and there cannot be duplicate batches, unless it refers to a rectified batch. Numbers must be reset every day. 2 - When “Type of file” =2, indicate the original batch number to be rectified, as submitted by the operator agent. | Numeric (5) | Yes | Daily uninterrupted sequence, there must be as many as daily files to be submitted from the Bets file. | 4 numeroLote (numberBatch) |
| CNPJ | Identification of the National Registry of Legal Persons (CNPJ) of the operator agent holder of the licence granted by SPA/MF, numbers only, including the verification digit. | Numeric (14) | Yes | CNPJ registered in the Federal Revenue Secretariat, numbers only. | 5 CNPJ |
| Brand | Identification of the brand that is exploring the operation, as is in the SPA/MF authorisation. | Text (100) | Yes | Brand associated to the CNPJ authorised to operate by SPA/MF. | 6 marca (brand) |
| Final batch tag | Identifies if the batch sent is the last “Sports Betting” type of file to be sent on the day. | Numeric (1) | Yes | 0 - No 1 - Yes | 7 idLoteFinal (idBatchFinal) |
| Date/Time file generation | Date/Time of the generation of the file. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes | Brasília Time Zone (UTC-3) | 8 dataHoraGeracao (dateTimeGeneration) |

#### DETAILS

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Bet ID | Unique alphanumeric identification through which the bet can be identified. | Text (20) | Yes | Identification assigned by the operator agent after the bet is effective. | 1 idAposta (idBet) |
| IP address | IP address of the electronic device on which the bet was placed. | Text (16) | Yes | ID address obtained from the registration into the betting system that the bettor completed to place the bet. | 2 enderecoIP (addressIP) |
| Place of origin of the bet | Place where the bet was placed, instantly determined by appropriate technology. | Numeric (7) | Yes | IBGE Municipality Codes | 3 localOrigemAposta (placeOriginBet) |
| CPF | Number of the Registry of Physical Person - CPF of the bettor. | Numeric (11) | Yes | - | 4 CPF |
| Type of Bet | It indicates whether the bet placed is simple, multiple or system. | Numeric (1) | Yes | 1 - Simple 2 - Multiple 3 - System | 5 tipoAposta (typeBet) |
| Bet Status | Information of the bet status (open, prized, not prized, suspended, cancelled) | Numeric (1) | Yes | 1 - Open 2 - Prized 3 - Not prized 4 - Suspended 5 - Cancelled | 6 statusAposta (statusBet) |
| Reason for Bet Suspension | It identifies the reason why the bet was suspended. | Numeric (1) | Yes, if “Bet Status” = 4 | 1 - Suspected fraud 2 - Event suspended 3 - Others | 6.1 motivoSuspensao (reasonSuspension) |
| Reason for Bet Cancellation | It identifies the reason why the bet was cancelled. | Numeric (1) | Yes, if “Bet Status” = 5 | 1 - Technical error 2 - Hints of fraud 3 - Event cancelled 4 - Others | 6.2 motivoCancelamento (reasonCancellation) |
| Code of Sport Discipline | Sport discipline offered by the operator to commercialise the bet. | Numeric (3) | Yes | Sport Discipline Table, as published in Annex VI of the Manual. | 7 codModalidade (codeDiscipline) |
| Sports Tournament | Name of the sports tournament, competition or exhibition, individual or collective, of which the betting object is part. | Text (100) | Yes | Name given to the sports tournament by the operator agent or official organiser entity of the sports tournament. Avoid special characters and accent marks. | 7.1 competicao (competition) |
| Betting Object Event | Name of the event, act, game or test with human interaction, individual or collective, including virtual, excluding those that exclusively involve people below eighteen years of age, with unknown result at the time of the bet. | Text (100) | Yes | Name given to the event, by the operator agent or official organiser entity of the sports tournament. | 7.2 eventoModalidade (eventDiscipline) |
| Event Status | It informs whether the event has been postponed, cancelled, delayed, ongoing, finalised or not started. | Numeric (1) | Yes | 1 - Postponed 2 - Cancelled 3 - Delayed 4 - Ongoing 5 - Finalised 6 - Not started | 7.3 statusEvento (statusEvent) |
| Amount of Markets | Total of betting markets in a unique bet. | Numeric (3) | Yes | - | 7.4 qtdMercado (quantityMarket) |
| Market Name | Identification of the betting market(s), such as “1x2”, “Draw no Bet”, “Exact Result”, “Over/Under”, “Handicap”. | Text (100) | Yes | Name given to the betting market by the betting operator agent. For each betting market, an identification must be included. | 7.5 nomeMercado (nameMarket) |
| Type of Betting Market | It identifies whether the bet was placed on the final result or on a difference in points of a sporting event (primary market). | Numeric (1) | Yes | 1 - Yes 2 - No | 7.5.1 tipoMercado (typeMarket) |
| Fixed Odd of the Market | Multiplication factor of the amount placed for bet that defines the sum to be received by the bettor, in case of being prized, for each unit of coin. The odd may vary, at the discretion of the operator agent, until the moment when the bet is placed, when it will remain fixed. | Numeric (3.2) | Yes | One odd must be reported per market. | 7.5.2 quotaFixaMercado (oddFixedMarket) |
| Fixed Odds of Prized Combination | Multiplication factor of the amount placed for bet that defines the sum to be received by the bettor, in case of being prized, for each unit of coin placed in the respective prized combination. The odd may vary, at the discretion of the operator agent, until the moment when the bet is placed, when it will remain fixed. | Numeric (3.2) | Yes, if “Type of Bet” equals 3 and “Bet Status” equals 2. | The fixed odd must be reported for the prized combination. | 9 quotaFixaMercado (oddFixedMarket) |
| Odd Total | It is the result of every multiplication factor of each market on which bets are placed. In case of prizing, the amount will be determined by the multiplication of the fixed odd by each coin unit placed. The odd may vary, at the discretion of the operator agent, until the moment when the bet is placed, when it will remain fixed. | Numeric (3.2) | Yes | - | 10 quotaFixaTotal (oddFixedTotal) |
| Bet Amount | Amount of the bet placed by the bettor, in Brazilian Reais | Numeric (8,2) | Yes | - | 11 valorAposta (amountBet) |
| Date/time of Bet | Date/time when the bet was placed by the bettor. Brasília - DF is the time zone considered. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes | Brasília Time Zone (UTC-3) | 12 dataHoraAposta (dateTimeBet) |
| Bettor Winnings | It is the difference between the amount of the prize and the amount placed, in Brazilian Reais. | Numeric (8,2) | Yes, if “Bet Status” = 2 (prized) | - | 13 ganhoApostador (winningBettor) |
| Cash Out Indicator | It indicates if the bettor has opted to cash out. | Numeric (1) | 1 - Yes 2 - No | - | 14 indicadorCashOut (indicatorCashOut) |
| Type of Cash Out | It indicates if the bettor has opted for partial or full cash out. If the bettor opts for full cash out, the bet must be settled. | Numeric (1) | Yes, if “Cash Out indicator” = 1 | 1 - Full 2 - Partial | 15 tipoCashOut (typeCashOut) |
| Amount of Cash Out | It indicates the amount paid to the bettor for the cash out, in Brazilian Reais. | Numeric (8,2) | Yes, if “Cash Out indicator” = 1 | - | 16 valorCashOut (amountCashOut) |
| Total Number of Sports Bets of the day | Total number of sports bets that were submitted on the day. Sum of the number of bets of each batch submitted of the "Sports Betting” file. | Numeric (10) | Yes, if the final batch tag equals 1. | - | 17 qtdTotalApostas (quantityTotalBets) |
| Total Amount of Sports Bets of the day | Addition of the amount of sports bets submitted during the day as contained in “Sports Betting” file, in Brazilian Reais. | Numeric (12,2) | Yes, if the final batch tag equals 1. | - | 18 valTotalApostas (amountTotalBets) |
| Justification of File rectification | In case of a rectifier file, submit the justification for the rectification of the original file. The rectified file must be only used in cases of error in the file. | Text (100) | Yes, if “Type of File” = 2 | - | 19 justificativaRetificacao (justificationRectification) |

#### TRAILER

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Digital Signature | Digital signature of the operator agent. | Text | Yes | It is constituted by the digital certificate identification, issuing body of the electronic certificate, name (Standard XML Dsig 1.0) Standard W3C of digital signature. | 20 ds:Signature |

## Annex VI – Online Games Betting

### FILE: ONLINE GAMES

### SUBMISSION: DAILY

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|

#### HEADER

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Tipo de Arquivo (Type of File) | Indicates whether the file is original or rectifier. There may only be one rectifier Type of File if there is one previous original file already sent and validated. | Numeric (1) | Yes | 1 - Original 2 - Rectifier | 1 tipoArquivo (typeFile) |
| Version | Reference to the XSD file version made available by SPA/MF, basis for file generation. | Text (10) | Yes | This attribute can be found in the root node and contains the XSD version. | 2 versao (version) |
| Date of the movement referred | 1 - In case of an original file, it is the date of the movement when the betting operator agent’s system implemented the registration, whether they are new registrations. 2 - In case of a rectifier file, it is the date of the movement referred to in the original file. | Date (YYYY-MM-DD) | Yes | Brasília Time Zone (UTC-3) | 3 dataMovimentoRef (dateMovementRef) |
| Batch Number | 1 - When “Type of file” =1, indicate the batch number to be submitted by the betting operator agent. It must be sequential and there cannot be duplicate batches, unless it refers to a rectified batch. Numbers must be reset every day. 2 - When “Type of file” =2, indicate the original batch number to be rectified, as submitted by the operator agent. | Numeric (5) | Yes | Daily uninterrupted sequence, there must be as many as daily files to be submitted from the Online Games file. | 4 numeroLote (numberBatch) |
| CNPJ | Identification of the National Registry of Legal Persons (CNPJ) of the operator agent, numbers only, including the verification digit. | Numeric (14) | Yes | CNPJ registered in the Federal Revenue Secretariat, numbers only. | 5 CNPJ |
| Brand | Identification of the brand that is exploring the operation, as is in the SPA/MF authorisation. | Text (100) | Yes | Brand associated to the CNPJ authorised to operate by SPA/MF. | 6 marca (brand) |
| Final Batch Tag | Identifies if the batch sent is the last “Online Games” type of file to be sent on the day. | Numeric (1) | Yes | 0 - No 1 - Yes | 7 loteFinal (batchFinal) |
| Date/Time file generation | Date/Time of the generation of the file. | Datetime (YYYY-MM-DD HH-MM-SS) | Yes | Brasília Time Zone (UTC-3) | 8 dataHoraGeracao (dateTimeGeneration) |

#### DETAILS

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| CPF | Number of the Registry of Physical Person - CPF of the bettor, as registered in the Federal Revenue Secretariat of Brazil. | Numeric (11) | Yes | - | 1 CPF |
| Number of Bets | Number of Bets placed by the bettor on online games during the day. | Numeric (6) | Yes | - | 2 qtdApostasJogoDia (quantityBetsGameDay) |
| Number of Bets per Game Type | Number of bets placed by the bettor on online games in the betting operator agent, per game type. | Numeric (6) | Yes | It contains one of the following attributes: 1 - Slot 2 - Crash game 3 - Roulette 4 - Bingo 5 - Live games 6 - Card game 7 - Others | 3 qtdApostasTipoJogo (quantityBetsTypeGame) |
| Game Title | Title of the online game on which the bettor placed a bet, with offered and referenced name in the game certification. | Text (100) | Yes | The name of online games that were target of bets during the day must be informed. | 3.1 tituloJogo (titleGame) |
| Game Total Time | Total time spent by the player on the online game, in hours. | Time (HH-MM-SS) | Yes | - | 4 tempoTotalApostasJogo (timeTotalBetsGame) |
| Total Amount of Bets in the Game | Total amount placed as bets by the bettor on the online game during the day. | Numeric (8.2) | Yes | - | 5 valorTotalApostasJogo (amountTotalBetsGame) |
| Bettor Winning on the Game | It is the difference between the total amount of prizes and the total amount placed as bets in the game, in Brazilian Reais. | Numeric (8,2) | Yes | This field will always be a positive figure. | 7 ganhoApostasJogo (winningBetsGame) |
| Bettor Losses on the Game | It is the difference between the total amount placed as bets and the winnings in the game, in Brazilian Reais. | Numeric (8,2) | Yes | This field will always be a positive figure. | 8 perdaApostasJogo (lossesBetsGame) |
| Number of Prizes | Number of prizes the bettor won per online games session of the day. | Numeric (4) | Yes | - | 6 qtdPremiosSessaoJogo (quantityPrizesSessionGame) |
| Session ID | Unique identification of the prized online game session. | Text (20) | Yes | One unique identification must be informed for each prized online game session of the day. | 6.1 idSessao (idSession) |
| Bettor Total Time of the Day | Total time spent by the player on online games, in hours, during one day. | Time (HH-MM-SS) | Yes | - | 4 tempoTotalApostadorJogoDia (timeTotalBettorGameDay) |
| Bettor Total Amount in Games | Total amount placed as bets by the bettor on online games during the day. | Numeric (8.2) | Yes | This field will always be a positive figure. | 5 valorTotalApostadorJogoDia (amountTotalBettorGameDay) |
| Bettor Winnings | It is the difference between the total amount of prizes and the total amount placed as bets in the game during the day, in Brazilian Reais. | Numeric (8,2) | Yes | This field will always be a positive figure. | 7 ganhoApostadorJogoDia (winningBettorGameDay) |
| Bettor Losses | It is the difference between the total amount placed as bets and the winnings in the day, in Brazilian Reais. | Numeric (8,2) | Yes | This field will always be a positive figure. | 8 perdaApostadorJogoDia (lossesBettorGameDay) |
| Total Number of Online Game Bets of the day | Total number of online game bets submitted on the day. Sum of the number of bets placed on online games of each batch submitted from “Online Games” file. | Numeric (10) | Yes, if the final batch tag equals 1. | - | 9 qtdTotalApostadoDia (quantityTotalBetDay) |
| Total Amount of Online Game Bets of the day | Sum of the amount of online game bets submitted during the day as contained in “Online Games” file, in Brazilian Reais. | Numeric (12,2) | Yes, if the final batch tag equals 1. | - | 10 valTotalApostadoDia (amountTotalBetDay) |
| Justification of File rectification | In case of a rectifier file, submit the justification for file rectification. The rectified file must be only used in cases of error in the file. | Text (100) | Yes, if “Type of File” = 2 | - | 11 justificativaRetificacao (justificationRectification) |

#### TRAILER

| Field Description | Format | Mandatory | Obs/Domain | XML indentation | XML Name Original (English meaning) |
|---|---|---|---|---|---|
| Digital Signature | Digital signature of the operator agent. | Text | Yes | It is constituted by the digital certificate identification, issuing body of the electronic certificate, name (Standard XML Dsig 1.0) Standard W3C of digital signature. | 12 ds:Signature |

## Annex VII – Sports Table

| Code | Sport |
|---|---|
| 1 | Athletics |
| 2 | Motorsport |
| 3 | Badminton |
| 4 | Baseball |
| 5 | Basketball |
| 6 | Beach tennis |
| 7 | Billiard/Pool |
| 8 | Bobsled |
| 9 | Bocce/Boules |
| 10 | Bowling |
| 11 | Boxing |
| 12 | Canoeing/Kayaking |
| 13 | Capoeira |
| 14 | Cycling |
| 15 | Cricket |
| 16 | Curling |
| 17 | Darts |
| 18 | Fencing |
| 19 |  |
| 20 | Bodybuilding |
| 21 | Floorball |
| 22 | Matkot |
| 23 | Football/Soccer |
| 24 | Beach Football |
| 25 | American Football |
| 26 | Futsal |
| 27 | Artistic Gymnastics |
| 28 | Golf |
| 29 | Weightlifting |
| 30 | Handball |
| 31 | Beach handball |
| 32 | Horse Riding |
| 33 | Field Hockey |
| 34 | Ice Hockey |
| 35 | Roller Hockey |
| 36 | Jiu-jitsu |
| 37 | Judo |
| 38 | Karate |
| 39 | Kickboxing |
| 40 | Kung fu |
| 41 | Powerlifting |
| 42 | Free Fighting |
| 43 | MMA |
| 44 | Motorcycling |
| 45 | Muay Thai |
| 46 | Swimming |
| 47 | Roller Skating |
| 48 | Sport Fishing |
| 49 | Polo |
| 50 | Waterpolo |
| 51 | Rowing |
| 52 | Rugby |
| 53 | Skateboarding |
| 54 | Skeleton |
| 55 | Snowboard |
| 56 | Softball |
| 57 | Squash |
| 58 | Sumo |
| 59 | Surfing |
| 60 | Taekwondo |
| 61 | Tennis |
| 62 | Table tennis |
| 63 | Target Archery |
| 64 | Shooting sport |
| 65 | Triathlon, Duathlon, Aquathlon |
| 66 | International Horse Racing |
| 67 | Sailing |
| 68 | Volleyball |
| 69 | Beach Volleyball |
| 70 | Wrestling |
| 999 | Other Sports |

In case of bets related to sports played by people with disabilities (PCD), Code 8 must be included on the left of the number of the table above. Thus, for example, for bets related to boules played by athletes with sight deficiencies, the code informed must be 89.