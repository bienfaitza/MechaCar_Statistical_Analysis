
## Linear Regression to Predict 
Using the dataset on suspension coils, I created a summary statistics table showing the suspension coil's PSI continuous variable across all manufacturing lots and the PSI metrics for each lot. To accomplish this, I first read the data csv file, created the summary table for all the manufacturing lots (the total_summary table), and then grouped the table by the manufacturing lot to produce the table for each lot (the lot_summary table).

```
SuspensionData <- read.csv(file='Suspension_Coil.csv',check.names=F,stringsAsFactors=F)

total_summary <- SuspensionData %>% summarize(Mean=mean(PSI), Median=median(PSI), Variance=var(PSI), SD=sd(PSI), .groups = 'keep')

lot_summary <- SuspensionData %>% group_by(Manufacturing_Lot) %>% summarize(Mean=mean(PSI), Median=median(PSI), Variance=var(PSI), SD=sd(PSI), .groups = 'keep')
```

The script produced the following tables:

Total Summary Statistics

![Total Summary](/Resources/totalsummary.PNG)

Per Lot Summary Statistics

![Lot Summary](/Resources/lotsummary.PNG)

The design specifications for the MechaCar suspension coils dictated that the variance of the suspension coils must not exceed 100 pounds per square inch. Based on these specifications, the current manufacturing data does meet the criteria for all the lots in total as the variance is 62.29. Individually, Lots 1 and 2 meet the specifications with variances of 0.98 and 7.47 respectively, but Lot 3 has a variance of 170.29 which well exceeds the maximum of 100 pounds per square inch.

## T-Tests on Suspension Coils
I performed t-tests to determine if all manufacturing lots and each lot individually was statistically different from the population mean of 1,500 pounds per square inch.

```
#t-test for all manufacturing lots
t.test(SuspensionData$PSI, mu=1500)

#t-test for lot 1
t.test(subset(SuspensionData$PSI, SuspensionData$Manufacturing_Lot == "Lot1"), mu=1500)
#t-test for lot 2
t.test(subset(SuspensionData$PSI, SuspensionData$Manufacturing_Lot == "Lot2"), mu=1500)
#t-test for lot 3
t.test(subset(SuspensionData$PSI, SuspensionData$Manufacturing_Lot == "Lot3"), mu=1500)
```

The script produced the following analysis:

T-Test for All Manufacturing Lots

![T-Test All](/Resources/ttest_all.PNG)

The t-test for all manufacturing lots had a p-value of 0.06, meaning that there is enough evidence to reject the null hypothesis. Therefore, the mean PSI of all manufacturing lots is statistically different from the population mean of 1,500 pounds per square inch.

T-Test for Lot 1

![T-Test Lot 1](/Resources/ttest_lot1.PNG)

The t-test for Lot 1 had a p-value of 1, meaning that there is not enough evidence to reject the null hypothesis. Therefore, the mean PSI of Lot 1 is not statistically different from the population mean of 1,500 pounds per square inch.

T-Test for Lot 2

![T-Test Lot 2](/Resources/ttest_lot2.PNG)

The t-test for Lot 2 had a p-value of 0.61, meaning that there is not enough evidence to reject the null hypothesis. Therefore, the mean PSI of Lot 2 is not statistically different from the population mean of 1,500 pounds per square inch.

T-Test for Lot 3

![T-Test Lot 3](/Resources/ttest_lot3.PNG)

The t-test for Lot 3 had a p-value of 0.04, meaning that there is enough evidence to reject the null hypothesis. Therefore, the mean PSI of Lot 3 is statistically different from the population mean of 1,500 pounds per square inch.

# Study Design
 It would be useful to perform a statistical study to compare the safety ratings of MechaCar vehicles against the safety ratings of vehicles from other manufacturers. The null hypothesis would be that MechaCar vehicles do not have statistically significant higher safety ratings than that of vehicles from other manufacturers, while the alternative hypothesis would be that MechaCar vehicles do have statistically significant higher safety ratings than that of vehicles from other manufacturers. 
