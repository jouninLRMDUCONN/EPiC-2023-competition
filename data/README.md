This is the default directory for storing data used in the `explain_data.ipynb` notebook.
If you want to run the notebook you need to either put the data here, or change data paths in code cells.

The dataset is allowed on the following route https://drive.google.com/drive/folders/1H61JMuD8IzcEzt8K2Hf-ra2bOyND639g?usp=sharing

## Preprocessing data

The preprocessing data is allowed on each scenario just in the same folder than the train and test data, with the name 'preprocessed'

This data contains the following data

IHR: Instantaneous heart rate 
PTT: Pulse transit time (from ecg to ppg)
TEMG, ZEMG, SEMG: linear envelope of the three muscles 
EDApha, EDAton: phasic and tonic component of EDA
RESP: respiratory rate
TEMP: skin temperature


With a sampling rate of 20Hz, based on the Annotation data sampling rate.

All the results and possible advances can be saved with the following recommendations from the Challenge team.

## 6. (Optional) Validation on subset of test data
As mentioned in Section 4 of this ReadMe, teams can divide their training set (e.g., into training and validation) if they would like. Nonetheless, many teams have asked if they can use a subset of the (hidden) test data to validate their models. Although we plan to keep the test data hidden until the conclusion of the challenge, teams can optionally send us up to three solutions to validate on a subset of the test data.

If you send us three solutions to validate on a subset of the test data, one of these solutions must be in the final submission repository. If you send us two or less solutions to validate on a subset of the test data, you may include a different solution in your final repository.

At the end of every business day (PST), we will perform a validation procedure on 50% of the test set and email you back the performance score. Instructions for submitting are below.

- Have the team leader send an email titled “EPiC23_[Team_name]_[Attempt_#]” to both stanislaw.saganowski@pwr.edu.pl and bartosz.perz@pwr.edu.pl 
- In this email, you can attach your results files with predictions. Alternatively, you can provide us a link to where these files are uploaded.
- Predictions should be in a zipped file with the same name as the email (e.g., EPiC23_Emognition_Attempt_1.zip). 
- The zipped file should be structured in the same way as final submissions, which are described in Section 7 of this ReadMe.
- Please do not password protect the file.

## 7. Final Submission Instructions
- Create a **Github repository** that includes the following:

	- **Your code with your solution.** Please ensure that your code is clean, well commented, and easy to reproduce. Make it in a way you would like to find when using someone else’s code.

	- **Result files with predictions.** Template files are located in `test/annotations` folders in each Scenario. Fill out the `arousal` and `valence` columns. Include result files in the `results` directory. Keep the original naming and structure of directories, e.g., `./results/scenario_2/fold_3/test/annotations/sub_0_vid_2.csv`.

	- **Dependencies file** with required libs and their versions.

	- **A short readme** introducing the team, explaining your approach, and describing the repository content and how to run the code. 
	- You can create a public repository, or send us an invitation to the private one. You should use a [CC-BY license](https://creativecommons.org/licenses/by/4.0/).

- Repositories will be cloned on **1 May 2023 10 am PT** into a single meta-repository with one branch per team. This meta-repository will be made publicly available.

- We will utilize the RMSE metric to assess the model performance. The final result will be obtained by calculating the mean score on all scenarios and dimensions (valence and arousal). The performance in each scenario will be assessed by mean RMSE in each fold.

- We will review all the repositories and replicate the top 3 submissions. If in doubt, we may contact the teams and request more information (e.g., model weights).
