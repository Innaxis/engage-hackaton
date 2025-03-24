# Engage Hackaton

## Extra resources
Initial presentation: https://docs.google.com/presentation/d/1Lr_10KhRx7dkQijB2XKxzLczSie2HN8c/

Live airport visualization: https://lemd.databeacon.io/

Email to submit your answers:  datahackathon@innaxis.aero

## Goal of the hackaton

* You  will be given a series of scenarios, in which we have selected a specific aircraft that is about to land.

* The ultimate goal of this hackathon is to predict the time that the aircraft will take from the last position reported to a specific point in the runway (called threshold point), in the time window provided.

* In this repo, you can find a sample with scenarios and their solutions, for you to start developing your models.

* During the Hackathon day 1 you will receive some checkpoint scenarios, and during day 2, you will receive the final scenarios, which will be the ones for you to solve, using the previously developed model. Both the sample, checkpoint and final scenarios will follow the same format.

## Further information

* Each scenario consists of a 2-minute window with data from the antenna.

* The airport chosen has 4 runways. In each scenario, we have labelled the runway used by each aircraft so you know which threshold point to use for each prediction.

## Submissions

### Schedule

Times are in Spain local time.

* Monday 24th 7pm (19:00): Checkpoint scenarios become available (you will be able to submit two different answers per team).
* Monday 24th 8pm (20:00): Deadline for checkpoint scenarios submissions.
* Tuesday 25th 12am (12:00): Final scenarios become available.
* Tuesday 25th 1pm (13:00): Deadline for final scenarios submissions.

### 1st submission: Monday 24th, 8pm

* This is not compulsory and won't affect your final score. But you can use it to test two different approaches and check your results with respect to the other teams.

* **You are allowed to submit two different solutions**. This way, you can try two different approaches and asses the results.

* You will need to submit a file with the same format as samples/sample_predictions_empty.csv, but with the checkpoint scenarios.

* We will submit a ranking with the results of this checkpoint. Each of the two solutions will be graded separately.

### 2nd and final submission: Tuesday 25th, 1pm

* One hour before the deadline, you will receive the final scenarios, for which you will have to send the predicted results.

* You will need to submit a file with the same format as samples/sample_predictions_empty.csv, but with the final scenarios.

## Files in this repo

* *runways.geojson*: The geometries of the airport runways.

* *score_metric.ipynb*: This is the metric that we will use to compute the scores. Your objective is to **minimize** the value of the metric.

* *thresholds.geojson*: The threshold points along with the runway that they belong to.

* *samples/*: This folder contains sample scenarios following the same format than the real scenarios that you will have to predict. You can use it to make sure that your model works with the scenario format.

    * *samples/sample_predictions_empty.csv*: This csv file contains the scenario list. Your goal will be to fill and submit the csv file with your predictions (but NOT this one, the one we will give you later with the real scenarios). It contains the following fields:

        * id_scenario: the id of a specific scenario. There will be a parquet file with the same name containing the scenario itself.

        * icao24: the ICAO transponder code of the specific aircraft. You can use this field to identify the aircraft that you have to predict.

        * runway: the identifier of the runway that the specific aircraft is going to land in. Use this field to select the correct threshold point for the predictions.

        * seconds_to_threshold: this column will be empty. Your goal is to fill it with your predictions. Remember to predict the time that it will take the aircraft to reach the threshold point from the time of the last position reported in the scenario.

    * *samples/sample_scenario_00.parquet* & *samples/sample_scenario_00.parquet*: These are the scenarios that you have to solve.

    * *samples/answers/sample_predictions_filled.csv*: This are the answers to the sample scenarios that we have provided. You will NOT have these for the real scenarios. This is only for you to know how the csv file has to be submitted. These answers are correct, so you can use them for training/validation if you like.

## Other considerations

* Be aware that the `ts` (UNIX timestamp) field is in **milliseconds**. The resulting datetimes should range from 2024-12-15 to 2025-03-15. You can cast the ts column to datetime with pandas as follows: `df["datetime"] = pd.to_datetime(df["ts"], unit="ms")`

* Although the time in the scenarios is in milliseconds, you have to submit your answers **in seconds**. Please mind the units and perform the conversions.

* Using external information that we have not provided is **NOT ALLOWED**.

* However, you can use [the AIP](https://aip.enaire.es/aip/contenido_AIP/AD/AD2/LEMD/LE_AD_2_LEMD_en.pdf). We recommend checking pages 34 and 35, but you can use any other information in that document.
