# Global Air Pollutant Forecasting Using Sequential Transfer Learning
This repository presents the code and structure for the MSc thesis “Global Air Pollutant Forecasting Using Sequential Transfer Learning: Addressing the Cold Start Problem.”
The project introduces a globally generalizable deep learning model capable of forecasting PM2.5 and PM10 air pollutant concentrations, even in data-scarce (cold-start) regions.

## Project Overview
Air pollution forecasting models typically rely on large, region-specific datasets. This creates two major challenges:
- Poor generalization – models trained in one region often fail in others.
- Cold-start problem – regions with limited historical air quality data cannot build effective models.

This project proposes a solution through Sequential Transfer Learning (STL), training a single LSTM-based model on PM datasets from seven world regions, allowing it to learn global temporal pollution patterns.

The result is a model that performs robustly even when the target region only has days or weeks of data available.

## Methodology
The diagram below shows the methodological overview.
![Methodology](https://github.com/ChrisDanAsh/Global-Air-Pollutant-Forecasting-Using-Sequential-Transfer-Learning/blob/7501f00575298afb7bf0173883fba0a707eccee8/Diagrams/Figure%201%20-%20Overview%20of%20Methodology%20v3.jpg)

### Data Pre-processing
The following steps were taken before the data was utilised in this study.
- Outlier removal via Seasonal-Trend decomposition using LOESS (STL)
- Missing value imputation using K-Nearest Neighbors (KNN)
- Filtering with a Butterworth low-pass filter
- Normalization (min–max)

This ensures high-quality inputs while preserving statistical characteristics.


### Sequential Transfer Learning Process
Instead of training on all regions at once, the model is trained on one region at a time, preserving learned weights after each stage. The models were trained on datasets across the globe, adding datasets starting from the US and moving roughly eastward, in the order shown below:
US → Colombia → UK → Uganda → India → China → Australia

This incremental training of the DL models via these datasets is the Sequential Transfer Learning process. 

## Results Summary
The STL method was applied to three ML models (LSTM, 1DCNN, GRU) and compared in three separate regions under data scarcity conditions. The performance of these models were compared against their baseline models to showcase the performance of the applied method. 

### Error Performance Line Graphs
The diagram below showcases the error performance of the three models over the various data scarcity conditions.
![Error Performance](https://github.com/ChrisDanAsh/Global-Air-Pollutant-Forecasting-Using-Sequential-Transfer-Learning/blob/8ab83a3fac18a533cc92531c3c3a6ed5d124021a/Diagrams/Figure%209%20-%20Error%20Performance%20vs%20Time%20Period%20line%20graphs.jpg)
DL models’ error versus data scarcity time period graphs: (a) DL models’ RMSE performance on the Korean dataset, (b) DL models’ MAE performance on the Korean dataset, (c)DL models’ RMSE performance on the
Mexican dataset, (d) DL models’ MAE performance on the Mexican dataset, (e) DL models’ RMSE performance on the Spanish dataset and (f) DL models’ MAE performance on the Spanish dataset.

### Average Improvement Bar Graph
The bar graph below shows the average improvement on each model, highlighting the effectiveness of the proposed method. 
![Average Performance Increase](https://github.com/ChrisDanAsh/Global-Air-Pollutant-Forecasting-Using-Sequential-Transfer-Learning/blob/8ab83a3fac18a533cc92531c3c3a6ed5d124021a/Diagrams/Figure%2011%20-%20Average%20Improvement%20of%20each%20model.jpg)

## Limitations & Future Work
- Hyperparameter tuning used random search; advanced optimizers (e.g., Bayesian, Optuna) may improve results.
- Fixed 50 epoch training could be replaced with adaptive methods like early stopping.
- Real-time deployment and inference speed were not evaluated.
- Some negative transfer occurred, highlighting the need for domain-selection strategies.
- External environmental features (weather, traffic, etc.) were not included and could enhance local accuracy.

## Conclusion
- Sequential transfer learning enabled the model to learn global PM patterns across seven world regions.
- The TL model consistently outperformed the baseline, with improvements from 25% to 99% across all scarcity levels.
- Accurate predictions were achieved even with extremely limited data (as little as 0.5 weeks).
- Results show strong generalization to unseen countries and effective handling of the cold-start problem.
- Findings support the existence of globally transferable pollution trends and provide a practical framework for regions with limited monitoring infrastructure.
