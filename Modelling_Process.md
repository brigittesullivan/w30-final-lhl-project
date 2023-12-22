# Modelling Process

Purpose:
The purpose of this document is to log all details of each model run during the modelling phase of this project. Including  exploration and refinement of models to improve results to be able to methodically replicate any model attempted. 
 
# Baselines:
## Prophet - Data Log
```py
{'train_data_source': 'data_log: logged original values', 'train_start_year': 1988, 'train_end_year': 2017, 'test_data_source': 'data_log: logged original values', 'test_start_year': 2018, 'test_end_year': 2019, 'model_params': 'Prophet()', '.fit()': 'train_data', 'model_fit_date': '2023-12-22 11:25', 'model_prediction_date:': '2023-12-22 11:26', 'Prediction range(num periods):': 24, 'Prediction frequency:': 'MS', 
'results': {
  'mse_train': 548425076145008.9, 
  'mse_test': 2683968874187328.5, 
  'rmse_train': 23418477.23796338, 
  'rmse_test': 51807034.987415835, 
  'mape_train': 0.31953629320855814}}
```
## AUTO ARIMA - Data Log
```py
'train_data_source': 'arima_train: logged original values from test_data, date as index',
 'train_start_year': 1988,
 'train_end_year': 2017,
 'model_data': 'arima_train',
 'model_params': {'random_state': 20, 'trace': True},
 'model_prediction_date:': '2023-12-22 12:10',
 'test_data_source': 'arima_test: logged original values from test_data, date as index',
 'test_start_year': 2018,
 'test_end_year': 2019,
 'best_arima_params': {'maxiter': 50,
  'method': 'lbfgs',
  'order': (2, 1, 2),
  'out_of_sample_size': 0,
  'scoring': 'mse',
  'scoring_args': {},
  'seasonal_order': (0, 0, 0, 0),
  'start_params': None,
  'suppress_warnings': True,
  'trend': None,
  'with_intercept': False},
 'results': {'mse_train': 1705112707308218.5,
  'mse_test': 6748189029322979.0,
  'rmse_train': 41293010.39290086,
  'rmse_test': 82147361.66988553,
  'mape_train': 0.3793135861817518,
  'mape_test': 0.4406118014368214}}
```
## Ensemble - mean of Prophet and Arima
```py
  {'description': 'Mean of previous prophet and arima predictions',
 'results': {'mse_train': 717028313456291.9,
  'mse_test': 1470508528629499.2,
  'rmse_train': 26777384.365473263,
  'rmse_test': 38347210.180526815,
  'mape_train': 0.25373467890051826,
  'mape_test': 0.28799336082629573},
 'model_prediction_date:': '2023-12-22 12:23'}
```
 ## Summary Baseline Models:

|Prophet|ARIMA|Ensemble| |
|:----|:----|:----|:----|
|mse_train|548,425,076,145,008.00|1,705,112,707,308,210.00|717,028,313,456,291.00|
|mse_test|2,683,968,874,187,320.00|6,748,189,029,322,970.00|1,470,508,528,629,490.00|
|rmse_train|23,418,477.24|41,293,010.39|26,777,384.37|
|rmse_test|51,807,034.99|82,147,361.67|38,347,210.18|
|mape_train|0.21|0.38|0.25|
|mape_test|0.32|0.44|0.29|

# Optimizing

## Find Best Params

```py 
{'description': 'Tuned Prophet Model, with CV',
 'params_options': {'changepoint_prior_scale': [0.001,
   0.101,
   0.201,
   0.301,
   0.401,
   0.5],
  'seasonality_prior_scale': [0.01, 1.01, 3.01, 5.0, 7.01, 10],
  'seasonality_mode': ['additive', 'multiplicative'],
  'yearly_seasonality': [True, False]},
 'cv_param_cutoffs': DatetimeIndex(['2018-01-01', '2019-01-01'], dtype='datetime64[ns]', freq=None),
 'cv_param_initial': '10593 days',
 'cv_param_period': '365 days',
 'cv_param_horizon': '365 days',
 'cv_param_parallel': 'processes',
 '.fit()': 'model_data_grouped',
 'model_prediction_date:': '2023-12-22 13:45',
 'best_params': {'changepoint_prior_scale': 0.101,
  'seasonality_prior_scale': 1.01,
  'seasonality_mode': 'multiplicative',
  'yearly_seasonality': True,
  'rmse': 32588005.106221694,
  'mape': 0.19241111774265449,
  'mape_idx': 30,
  'rmse_idx': 30}}
```

## Model using best params

```py
{'description': 'Predictions using best params and cv',
 'train_data_source': 'model_data_grouped: original values',
 'train_start_year': 1988,
 'train_end_year': 2017,
 'test_data_source': 'model_data_grouped: original values',
 'test_start_year': 2018,
 'test_end_year': 2019,
 'model_params': {'changepoint_prior_scale': 0.101,
  'seasonality_prior_scale': 1.01,
  'seasonality_mode': 'multiplicative',
  'yearly_seasonality': True,
  'rmse': 32588005.106221694,
  'mape': 0.19241111774265449,
  'mape_idx': 30,
  'rmse_idx': 30},
 '.fit()': 'model_data_grouped',
 'model_fit_date': '2023-12-22 14:11',
 'cv_param_cutoffs': DatetimeIndex(['2018-01-01', '2019-01-01'], dtype='datetime64[ns]', freq=None),
 'cv_param_initial': '10593 days',
 'cv_param_period': '365 days',
 'cv_param_horizon': '365 days',
 'cv_param_parallel': 'processes',
 'model_prediction_date:': '2023-12-22 14:11',
 'Prediction range(num periods):': 24,
 'Prediction frequency:': 'MS',
 'results': {'Prophet-Best': {'mse_train': 442878256290016.7,
   'mse_test': 383085492245001.56,
   'rmse_train': 21044672.872012448,
   'rmse_test': 19572569.89373142,
   'mape_train': 0.2735435107732697,
   'mape_test': 0.10547302594607018}}}
   ```

   ** to get seperate metrics for test and train... make predictions, then manually split results into train period and test period. ? 
   MAPE test lower! Very good news! 
   * using original values resulted in better predictions

## Find Best Params using Data not adjusted for inflation and not Log(x)
```py
{'description': 'Predictions using best params and cv on us data not adjusted for inflation or log',
 'train_data_source': 'us data: unindexed no log',
 'train_start_year': 1988,
 'train_end_year': 2017,
 'test_data_source': 'us data: unindexed no log',
 'test_start_year': 2018,
 'test_end_year': 2019,
 'model_params': {'changepoint_prior_scale': 0.101,
  'seasonality_prior_scale': 1.01,
  'seasonality_mode': 'multiplicative',
  'yearly_seasonality': True,
  'rmse': 26305292.84164052,
  'mape': 0.17541140467660435},
 'model_fit_date': '2023-12-22 14:37',
 '.fit()': 'us_data',
 'cv_param_cutoffs': DatetimeIndex(['2018-01-01', '2019-01-01'], dtype='datetime64[ns]', freq=None),
 'cv_param_initial': '10593 days',
 'cv_param_period': '365 days',
 'cv_param_horizon': '365 days',
 'cv_param_parallel': 'processes',
 'model_prediction_date:': '2023-12-22 14:37',
 'Prediction range(num periods):': 24,
 'Prediction frequency:': 'MS'}
 ```

## predict again but with values NOT adjusted for inflation.

   ```py
   {'description': 'Predictions using best params and cv on us data not adjusted for inflation or log',
 'train_data_source': 'us data: unindexed no log',
 'train_start_year': 1988,
 'train_end_year': 2017,
 'test_data_source': 'us data: unindexed no log',
 'test_start_year': 2018,
 'test_end_year': 2019,
 'model_params': {'changepoint_prior_scale': 0.101,
  'seasonality_prior_scale': 1.01,
  'seasonality_mode': 'multiplicative',
  'yearly_seasonality': True,
  'rmse': 26305292.84164052,
  'mape': 0.17541140467660435},
 'model_fit_date': '2023-12-22 14:37',
 '.fit()': 'us_data',
 'cv_param_cutoffs': DatetimeIndex(['2018-01-01', '2019-01-01'], dtype='datetime64[ns]', freq=None),
 'cv_param_initial': '10593 days',
 'cv_param_period': '365 days',
 'cv_param_horizon': '365 days',
 'cv_param_parallel': 'processes',
 'model_prediction_date:': '2023-12-22 14:37',
 'Prediction range(num periods):': 24,
 'Prediction frequency:': 'MS',
 'results': {'Prophet-Best': {'mse_train': 1415017803445176.2,
   'mse_test': 1182226568181031.2,
   'rmse_train': 37616722.39104806,
   'rmse_test': 34383521.75361086,
   'mape_train': 0.3654134014712997,
   'mape_test': 0.17204976308666972}}}
   ```

   Results higher than previous test when values are adjusted to todays dollar. 