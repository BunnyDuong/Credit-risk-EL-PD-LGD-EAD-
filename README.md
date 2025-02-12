# Credit risk EL PD LGD EAD-

In this project, I build an expected loss model (EL = PD X LGD X EAD)
The data extracted from (https://www.kaggle.com/datasets/adarshsng/lending-club-loan-data-csv) that has ~2.6M rows

1. PD model
- General processing of data
  
- Compute Weight of Evidence and Information value for categorical and continuous variables. From WoE, IV as well as the distribution of data, I categorize data into different buckets
<img width="232" alt="WoE" src="https://github.com/user-attachments/assets/264c5b01-b4db-4881-b951-cbe446deef94" />
Example: Plotting of WoE by home_ownership

- Training model with logistic regression in combination with p-value. After this step, we keep variable that has meaningful p-value
  
- Testing: model returns good result as the accuracy ~0.98
![image](https://github.com/user-attachments/assets/cac32805-0f40-47a4-b9cd-9ce68cf4cfcb)

- Finally, we compute the probability of default

2. LGD and EAD models
2.1 LGD model
- Compute recovery_rate based on recovery amount. I found out the values having recovery rate of 0 is more than half of values. Therefore, I break this part into 2 models:
    * Logistics regression model to predict if recovery_Rate is 0 or not (in combination with p-value evaluation)
    * Linear regression model to predict the value of recovery_rate if logistic regression predicts that recovery rate is not 0
2.2 EAD model
- Depedent variable: credit conversion factor (credit conversion factor calculated as equal to (funded_amount - total recovered principal)/ funded_amount)
- Using Linear regression
- Correlation between the actual and predicted values is good (~0.51)

3. EL model
The Expected loss model computed as EL = PD X LGD X EAD
