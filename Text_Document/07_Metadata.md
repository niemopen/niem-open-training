```
	nc:Person
		nc:PersonBirthDate
			nc:Date
		nc:PersonName
			nc:PersonGivenName
			nc:PersonMiddleName
			nc:PersonSurName
	j:Crash
		nc:ActivityDate
			nc:Date
		j:CrashPerson
			j:CrashPersonInjury
				nc:InjuryDescriptionText
				j:InjurySeverityCode
	j:PersonChargeAssociation
		nc:Person
		j:Charge
	ext:Charge
		j:ChargeDescriptionText
		j:ChargeFelonyIndicator
+	nc:Metadata
+		j:MetadataAugmentation
+			j:CriminalInformationIndicator
```
