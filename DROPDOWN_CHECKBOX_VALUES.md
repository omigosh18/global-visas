# Dropdown, Checkbox & Radio Button Values Reference

Complete reference of every possible value for every dropdown, radio button, and checkbox across all 22 form steps. For use by the automation engineer when building n8n workflows.

> **Webhook note:** All `yes`/`no` radio values are normalized to `"Yes"` / `"No"` strings in the outgoing webhook payload, unless otherwise noted.

---

## Countries List (used across many dropdowns)

The same list is used for all country dropdowns throughout the form:

`Afghanistan`, `Albania`, `Algeria`, `Argentina`, `Armenia`, `Australia`, `Austria`, `Azerbaijan`, `Bahrain`, `Bangladesh`, `Belarus`, `Belgium`, `Bolivia`, `Bosnia and Herzegovina`, `Brazil`, `Brunei`, `Bulgaria`, `Cambodia`, `Cameroon`, `Canada`, `Chile`, `China`, `Colombia`, `Croatia`, `Cuba`, `Cyprus`, `Czech Republic`, `Denmark`, `Ecuador`, `Egypt`, `Estonia`, `Ethiopia`, `Fiji`, `Finland`, `France`, `Georgia`, `Germany`, `Ghana`, `Greece`, `Hong Kong`, `Hungary`, `Iceland`, `India`, `Indonesia`, `Iran`, `Iraq`, `Ireland`, `Israel`, `Italy`, `Jamaica`, `Japan`, `Jordan`, `Kazakhstan`, `Kenya`, `Kuwait`, `Laos`, `Latvia`, `Lebanon`, `Libya`, `Lithuania`, `Luxembourg`, `Macau`, `Malaysia`, `Maldives`, `Malta`, `Mexico`, `Mongolia`, `Morocco`, `Myanmar`, `Nepal`, `Netherlands`, `New Zealand`, `Nigeria`, `North Korea`, `Norway`, `Oman`, `Pakistan`, `Palestine`, `Panama`, `Papua New Guinea`, `Peru`, `Philippines`, `Poland`, `Portugal`, `Qatar`, `Romania`, `Russia`, `Saudi Arabia`, `Serbia`, `Singapore`, `Slovakia`, `Slovenia`, `Somalia`, `South Africa`, `South Korea`, `Spain`, `Sri Lanka`, `Sudan`, `Sweden`, `Switzerland`, `Syria`, `Taiwan`, `Thailand`, `Tonga`, `Tunisia`, `Turkey`, `Ukraine`, `United Arab Emirates`, `United Kingdom`, `United States`, `Uruguay`, `Uzbekistan`, `Vanuatu`, `Venezuela`, `Vietnam`, `Yemen`, `Zimbabwe`

---

## Australian States List (used in Step 9, Step 11)

`Australian Capital Territory`, `New South Wales`, `Northern Territory`, `Queensland`, `South Australia`, `Tasmania`, `Victoria`, `Western Australia`

---

## Companion / Family / Contact Relationship List (used in Steps 5, 8, 9)

`Aunt`, `Brother`, `Business associate`, `Child`, `Cousin`, `Daughter`, `Son in law`, `Fiance/ fiancee`, `Friend`, `Grandchild`, `Grandparent`, `Mother/Father in law`, `Nephew`, `Niece`, `Parent`, `Sister`, `Sister/Brother in law`, `Spouse / De facto partner`, `Step child`, `Step parent`, `Step brother`, `Step sister`, `Uncle`

---

## Step 1: Terms and Conditions

| Field | Type | Values |
|-------|------|--------|
| `termsAccepted` | Checkbox | `true` / `false` (sent as `"Yes"` / `"No"` in webhook) |

---

## Step 2: Application Context

| Field | Type | Values |
|-------|------|--------|
| `outsideAustralia` | Radio | `"yes"` / `"no"` |
| `currentLocation` | Dropdown | Full countries list (see above) |
| `legalStatus` | Dropdown | `"Citizen"`, `"Permanent Resident"`, `"Visitor"`, `"Student"`, `"Work Visa"`, `"No Legal Status"`, `"Other"` |
| `visaStream` | Radio | `"business"`, `"frequent"`, `"sponsored"`, `"tourist"` |
| `frequentPurpose` | Radio (if visaStream = `"frequent"`) | `"business"`, `"tourism"` |
| `visitReasons` | Multi-select dropdown | `"Business"`, `"Tourism"`, `"Family Visit"`, `"Study"`, `"Religious Event"`, `"Other"` |
| `specialCategory` | Radio | `"yes"` / `"no"` |
| `specialCategoryType` | Radio (if specialCategory = `"yes"`) | `"foreign_gov"`, `"un_laissez"`, `"exempt_group"` |
| `lengthOfStay` / `furtherStayLength` | Dropdown | `"Up to 3 months"`, `"Up to 6 months"`, `"Up to 12 months"` |
| `groupProcessing` | Always disabled | `"No"` (always fixed) |
| `groupType` | Dropdown (if group travel) | `"Entertainment"`, `"Family"`, `"Friends"`, `"Incentive Tour"`, `"School / Study"`, `"Sports Team / Sports Event"`, `"Work / Employer"`, `"Other"` |

**Notes:**
- `visitReasons` allows multiple selections; sent as comma-separated string in webhook (e.g. `"Tourism, Business, Study"`)
- `specialCategoryType` labels: `"foreign_gov"` = Travelling as a foreign government representative; `"un_laissez"` = Travelling on a United Nations Laissez-Passer; `"exempt_group"` = Member of an exempt group

---

## Step 3: Applicant Details

| Field | Type | Values |
|-------|------|--------|
| `sex` | Radio | `"female"`, `"male"`, `"other"` |
| `birthCountry` | Dropdown | Full countries list |
| `relationshipStatus` | Dropdown | `"De Facto"`, `"Divorced"`, `"Engaged"`, `"Married"`, `"Never Married"`, `"Separated"`, `"Widowed"` |
| `hasOtherNames` | Radio | `"yes"` / `"no"` |
| `citizenOfOtherCountry` | Radio | `"yes"` / `"no"` |
| `hasNationalIdCard` | Radio | `"yes"` / `"no"` |
| `isPacificAustraliaCardHolder` | Radio | `"yes"` / `"no"` |
| `hasGrantNumber` | Radio | `"yes"` / `"no"` |
| `hasOtherPassports` | Radio | `"yes"` / `"no"` |
| `hasOtherIdentityDocs` | Radio | `"yes"` / `"no"` |
| `hasHealthExamination` | Radio | `"yes"` / `"no"` |

**Other Names table — `reason` field:**

`"Deed poll"`, `"Marriage"`, `"Other"`

**Other Travel Documents table — `docType` field:**

`"DFTTA"`, `"Immicard"`, `"Passport"`, `"PL056(M56)"`, `"Titre de voyage"`, `"Other travel document"`

**Other Identity Documents table — `docType` field:**

`"Birth certificate"`, `"Driver's licence"`, `"National ID card"`, `"Social security card"`, `"Tax file number"`, `"Other"`

---

## Step 4: Critical Data Confirmation

> This step appears as Step 4 in the form flow (immediately after Applicant Details). Navigation skips step number 14 — goes from Step 13 directly to Step 15.

| Field | Type | Values |
|-------|------|--------|
| `criticalDataConfirmed` | Radio | `"yes"` / `"no"` |

---

## Step 5: Travelling Companions (Passport Details / Country of Passport)

| Field | Type | Values |
|-------|------|--------|
| `countryOfPassport` | Dropdown | Full countries list |
| `citizenOfPassportCountry` | Radio | `"yes"` / `"no"` |
| `nationalityOfHolder` | Dropdown | Full countries list |

---

## Step 5: Travelling Companions

| Field | Type | Values |
|-------|------|--------|
| `hasTravellingCompanions` | Radio | `"yes"` / `"no"` |
| Companion `relationship` | Dropdown | Companion/Family Relationship list (see above) |
| Companion `sex` | Radio | `"female"`, `"male"`, `"other"` |

---

## Step 6: Contact Details

| Field | Type | Values |
|-------|------|--------|
| `usualCountryOfResidence` | Dropdown | Full countries list |
| `departmentOffice` | Dropdown | See list below |
| `residentialCountry` | Dropdown | Full countries list |
| `postalSameAsResidential` | Radio | `"yes"` / `"no"` |

**Department Office options:**

`"Bangladesh, Dhaka"`, `"Brazil, Brasilia"`, `"Cambodia, Phnom Penh"`, `"Canada, Ottawa"`, `"Chile, Santiago de Chile"`, `"China, Beijing"`, `"China, Guangzhou"`, `"China, Hong Kong"`, `"China, Shanghai"`, `"Colombia, Bogota"`, `"Egypt, Cairo"`, `"Fiji, Suva"`, `"Germany, Berlin"`, `"India, Bengaluru"`, `"India, New Delhi"`, `"Indonesia, Jakarta"`, `"Iran, Tehran"`, `"Israel, Tel Aviv"`, `"Jordan, Amman"`, `"Kenya, Nairobi"`, `"Malaysia, Kuala Lumpur"`, `"Myanmar, Yangon"`, `"New Zealand, Wellington"`, `"Pakistan, Islamabad"`, `"Papua New Guinea, Port Moresby"`, `"Philippines, Manila"`, `"Republic of Turkiye, Ankara"`, `"Serbia, Belgrade"`, `"Singapore"`, `"South Africa, Pretoria"`, `"South Korea, Seoul"`, `"Sri Lanka, Colombo"`, `"Thailand, Bangkok"`, `"Timor-Leste, Dili"`, `"United Arab Emirates, Dubai"`, `"United Kingdom, London"`, `"United States, Washington"`, `"Vietnam, Hanoi"`, `"Vietnam, Ho Chi Minh City"`

---

## Step 7: Authorised Recipient

| Field | Type | Values |
|-------|------|--------|
| `authorisedRecipient` | Radio | `"no"`, `"registered_migration_agent"`, `"legal_practitioner"`, `"another_person"` |

**Value labels:**
- `"no"` — No
- `"registered_migration_agent"` — Yes, a registered migration agent
- `"legal_practitioner"` — Yes, a legal practitioner
- `"another_person"` — Yes, another person

---

## Step 8: Non-Accompanying Family Members

| Field | Type | Values |
|-------|------|--------|
| `hasNonAccompanyingMembers` | Radio | `"yes"` / `"no"` |
| Member `relationship` | Dropdown | Companion/Family Relationship list (see above) |
| Member `sex` | Radio | `"female"`, `"male"`, `"other"` |
| Member `countryOfBirth` | Dropdown | Full countries list |

---

## Step 9: Entry to Australia

| Field | Type | Values |
|-------|------|--------|
| `lengthOfStay` | Dropdown | `"Up to 3 months"`, `"Up to 6 months"`, `"Up to 12 months"` |
| `multipleEntry` | Radio | `"yes"` / `"no"` |
| `willStudy` | Radio | `"yes"` / `"no"` |
| `hasAustraliaContacts` | Radio | `"yes"` / `"no"` |
| Contact `relationship` | Dropdown | Companion/Family Relationship list (see above) |
| Contact `sex` | Radio | `"female"`, `"male"`, `"other"` |
| Contact `residencyStatus` | Dropdown | `"Australian citizen"`, `"Australian permanent resident"`, `"Australian temporary resident (student)"`, `"Australian temporary resident (visitor)"`, `"Australian temporary resident (work visa)"`, `"Other"`, `"Unknown"` |
| Contact `state` | Dropdown (if country = Australia) | Australian States list (see above) |

---

## Step 10: Previous Travel to Australia

| Field | Type | Values |
|-------|------|--------|
| `previouslyTravelledToAustralia` | Radio | `"yes"` / `"no"` |
| `previouslyAppliedForVisa` | Radio | `"yes"` / `"no"` |

---

## Step 11: Employment Details

| Field | Type | Values |
|-------|------|--------|
| `employmentStatus` | Dropdown | `"Employed"`, `"Self employed"`, `"Unemployed"`, `"Retired"`, `"Student"`, `"Other"` |
| `empOccupationGrouping` | Dropdown (if Employed or Self employed) | `"Managers"`, `"Professionals"`, `"Technicians and Trades Workers"`, `"Community and Personal Service Workers"`, `"Clerical and Administrative Workers"`, `"Sales Workers"`, `"Machinery Operators and Drivers"`, `"Labourers"` |
| `empOrgCountry` | Dropdown | Full countries list |
| `empOrgState` | Dropdown (if country = Australia) | Australian States list (see above) |

---

## Step 12: Financial Support

| Field | Type | Values |
|-------|------|--------|
| `fundingSource` | Radio | `"Self funded"`, `"Supported by current overseas employer"`, `"Supported by other organisation"`, `"Supported by other person"` |
| `employerSupportType` | Radio (if employer funded) | `"Financial"`, `"Accommodation"`, `"All costs"`, `"Other"` |
| `orgSupportType` | Radio (if org funded) | `"Financial"`, `"Accommodation"`, `"All costs"`, `"Other"` |
| `fundingOrgCountry` | Dropdown (if org funded) | Full countries list |
| `personFundedRelationship` | Dropdown (if person funded) | Companion/Family Relationship list (see above) |
| `personSupportType` | Radio (if person funded) | `"Financial"`, `"Accommodation"`, `"All costs"`, `"Other"` |

---

## Step 13: Additional Details

| Field | Type | Values |
|-------|------|--------|
| `hasAdditionalDetails` | Radio | `"Yes"` / `"No"` |

---

## Step 15: Visit Relatives

| Field | Type | Values |
|-------|------|--------|
| `hasVisitRelatives` | Radio | `"yes"` / `"no"` |
| Relative `relationship` | Dropdown | `"Aunt"`, `"Brother"`, `"Child"`, `"Cousin"`, `"Daughter"`, `"De facto partner"`, `"Father"`, `"Friend"`, `"Grandchild"`, `"Grandparent"`, `"Mother"`, `"Nephew"`, `"Niece"`, `"Sister"`, `"Son"`, `"Spouse"`, `"Step child"`, `"Step parent"`, `"Uncle"`, `"Other"` |

---

## Step 16: Health Declarations

All fields are Radio with values `"yes"` / `"no"`:

| Field | Description |
|-------|-------------|
| `healthVisitedOutside` | Visited or lived outside country of passport for 3+ months |
| `healthEnterHospital` | Required to enter hospital or other institution |
| `healthWorkHealthcare` | Intends to work in healthcare, aged care, child care or disability services |
| `healthAgedCare` | Intends to work in aged care |
| `healthTuberculosis` | Has or has had tuberculosis |
| `healthMedicalCosts` | Would require medical costs beyond those expected |
| `healthOngoingCare` | Requires ongoing medical care |

---

## Step 17: Character Declarations

All fields are Radio with values `"yes"` / `"no"`:

| Field | Description |
|-------|-------------|
| `charConvicted` | Has been convicted of any offence |
| `charOffenceCharged` | Has been charged with any offence |
| `charAcquittedInsanity` | Has been acquitted on grounds of insanity |
| `charArrestWarrant` | Is subject to an outstanding arrest warrant |
| `charWarCrimes` | Has been involved in or associated with war crimes |
| `charDomesticViolence` | Has had a domestic violence order |
| `charSexualOffence` | Has been convicted of or charged with a sexual offence |
| `charSexOffenderRegister` | Is registered or required to be on a sex offender register |
| `charDeported` | Has been deported or removed from any country |
| `charVisaOverstay` | Has overstayed a visa |
| `charCriminalConduct` | Has engaged in criminal conduct |
| `charPeopleSmuggling` | Has been involved in people smuggling |
| `charViolenceOrg` | Has been a member of a violent organisation |
| `charNationalSecurity` | Has been involved in activities against national security |
| `charOutstandingDebts` | Has outstanding debts to any government |
| `charMilitaryService` | Has served in a military force |
| `charMilitaryTraining` | Has received military or intelligence training |
| `charUnfitPlead` | Has been found unfit to plead |

---

## Step 18: Visa History

All fields are Radio with values `"yes"` / `"no"`:

| Field | Description |
|-------|-------------|
| `visaHeldVisa` | Has previously held an Australian visa |
| `visaNonComplied` | Has not complied with conditions of an Australian visa |
| `visaRefusedCancelled` | Has had an Australian visa refused or cancelled |

---

## Step 19: Additional Declarations

All fields are Radio with values `"Yes"` / `"No"`:

| Field | Description |
|-------|-------------|
| `declAccurateInfo` | Understands that providing false or misleading information is a serious offence |
| `declHealthAssessment` | Consents to undergoing a health assessment if required |
| `declCooperateAuthorities` | Agrees to cooperate with Australian authorities for identity verification |
| `declConditionsUnderstood` | Understands that visa conditions may restrict activities and that breaches may cause cancellation |

---

## Step 20: Declarations

All fields are Radio with values `"Yes"` / `"No"`:

| Field | Description |
|-------|-------------|
| `declNoWork` | Will not work unlawfully in Australia |
| `declNoStudyTraining` | Will not study or undertake training unlawfully |
| `declLeaveAustralia` | Will leave Australia before visa expires |
| `declNoFurtherStay` | Will not apply to stay further without permission |
| `declInformChanges` | Will inform the department of any changes in circumstances |
| `declCompleteCorrect` | Certifies that the information provided is complete and correct |
| `declReadUnderstood` | Has read and understood all questions |
| `declFraudulentRefusal` | Understands consequences of fraudulent applications (refusal) |
| `declFraudulentCancellation` | Understands consequences of fraudulent applications (cancellation) |
| `declUnlawfulNonCitizen` | Understands consequences of becoming an unlawful non-citizen |
| `declPersonalInfo` | Consents to the use of personal information |
| `declPrivacyNotice` | Has read the privacy notice |
| `declBiometricConsent` | Consents to providing biometric information |
| `declFingerprints` | Consents to fingerprinting |
| `declFingerprintsLawEnforcement` | Understands fingerprints may be shared with law enforcement |
| `declLawEnforcementConsent` | Consents to sharing information with law enforcement agencies |

---

## Step 21: Review

No user-selectable fields — displays a read-only summary of all previously entered data.

---

## Step 22: Attach Documents

Document category selections (upload slots):

| Category | Type |
|----------|------|
| Travel Document | Required |
| National ID | Required |
| Previous Travel | Required |
| Family Register | Recommended |
| Tourism Evidence | Recommended |
| Financial Evidence | Recommended |

---

## Quick Reference: All Yes/No Radio Fields

The following fields all use `"yes"` / `"no"` as raw values (normalized to `"Yes"` / `"No"` in webhook):

`outsideAustralia`, `specialCategory`, `hasTravellingCompanions`, `citizenOfPassportCountry`, `hasNonAccompanyingMembers`, `multipleEntry`, `willStudy`, `hasAustraliaContacts`, `previouslyTravelledToAustralia`, `previouslyAppliedForVisa`, `hasVisitRelatives`, `postalSameAsResidential`, `healthVisitedOutside`, `healthEnterHospital`, `healthWorkHealthcare`, `healthAgedCare`, `healthTuberculosis`, `healthMedicalCosts`, `healthOngoingCare`, `visaHeldVisa`, `visaNonComplied`, `visaRefusedCancelled`

The following fields use `"Yes"` / `"No"` (capitalized) directly:

`criticalDataConfirmed`, `hasOtherNames`, `citizenOfOtherCountry`, `hasNationalIdCard`, `isPacificAustraliaCardHolder`, `hasGrantNumber`, `hasOtherPassports`, `hasOtherIdentityDocs`, `hasHealthExamination`, `hasAdditionalDetails`, `declAccurateInfo`, `declHealthAssessment`, `declCooperateAuthorities`, `declConditionsUnderstood`, `declNoWork`, `declNoStudyTraining`, `declLeaveAustralia`, `declNoFurtherStay`, `declInformChanges`, `declCompleteCorrect`, `declReadUnderstood`, `declFraudulentRefusal`, `declFraudulentCancellation`, `declUnlawfulNonCitizen`, `declPersonalInfo`, `declPrivacyNotice`, `declBiometricConsent`, `declFingerprints`, `declFingerprintsLawEnforcement`, `declLawEnforcementConsent`
