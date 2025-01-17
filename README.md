# Setting Up This Git Repository
Here are the basic steps to get this Git repository on your local machine so you can work on this project. Anything written in the style %VARIABLE% must be replaced when executing. 

0. Download Git for Windows in some form (if you are using Linux, then Git is already installed). You have two options:
    * [Git for Windows](https://gitforwindows.org/): This will install the Git BASH terminal, a Unix terminal emulator that you will use for all your Git management.
    * [PowerShell 7](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.3): This will install PowerShell 7, the most recent form of Windows PowerShell. Then you will need to [install Git using Posh-git](https://git-scm.com/book/en/v2/Appendix-A%3A-Git-in-Other-Environments-Git-in-PowerShell)

1. Determine where you want to create the EPiC-2023_competition folder. In your terminal, navigate to your desired directory using the command "cd %PATH%" (replace %PATH% with the directory). You do not need to make a EPiC_2023Chanllenge folder, one will be created by Git.

2. Create your local copy of the Git repository. Once in the desired directory, type "git clone https://github.uconn.edu/lrm22005/EPiC-2023_competition.git" to create the Git repository in a folder at %PATH%/EPiC-2023_competition/. You may have to sign in using your GitHub user. If you have any issues, try running your terminal as an Administrator.

3. Open the EPiC-2023-competition folder in your terminal using the "cd" command. You should see "%PATH%/EPiC-2023_competition [main]>" in your terminal. This means you have the repo downloaded and have currently loaded the Main branch.

4. Create your own branch of the Git repository. Type "git checkout -b %YOURNAME%" to create a branch named %YOURNAME% and open it. This will be your version of the code. You should see "%PATH%/EPiC-2023_competition [%YOURNAME%]>" in your terminal.

5. Push your newly created branch to the remote repository. Type "git add ." to add everything in your current folder (think putting everything in a box), then type "git commit -m "%YOUR COMMIT MESSAGE%"" with your own commit message (think addressing and labeling the box), then type "git push --set-upstream origin %YOURNAME%" to push your branch to remote (think sending the box). Check that the commit pushed properly by refreshing this page and looking for your branch under Branches.

Git will allow us to all work collectively on code and keep versions managed. Please keep your models in the Models folder, your feature extraction in the Features folder, and your prepocessing and cleaning in the Preprocessing folder. Any cleaning or preprocessing should be able to read from raw .mat files. We can discuss standards for features and model formats later.

When using Git, everytime you want to push a change you should use similar steps to 5. above. Type "git add ." to add everything in your current folder, then type "git commit -m "%YOUR COMMIT MESSAGE%"" with your own commit message, then type "git push" to push your branch to remote. When you have any major updates that you would like to share with everyone, please let Luis know and he will merge the code with the Main branch. 

Whenever you would like to download updated code from the Main branch, use the following commands:

    git checkout main
    git pull 
    git checkout %YOURNAME%
    git merge main
This will switch your local repo to the main branch, download it, switch back to your branch, and then move changes into your branch. It will only update code that has the same file name as what you have in your folder as well as add any new files. It should not modify any code you have that is not in the Main branch. In case of any merge conflicts, you will have to manually determine which code is the most up to data that you want to keep.

# EPiC 2023: The Emotion Physiology and Experience Collaboration

This repository contains data, information, and helpful code for the [EPiC 2023 competition](https://epic-collab.github.io/competition/).

## 1. The goal of the EPiC 2023 competition
We are piloting a shared task that aims to (1) establish the best approaches for predicting moment-to-moment feelings of valence and arousal from multi-modal measures of physiology, (2) compare how model accuracy scores vary across different validation scenarios, and (3) promote open science.


## 2. Your task
The task is to predict continuous, moment-to-moment, self-reported ratings of valence and arousal based on multi-modal measures of physiology. Formally, this is a regression problem. There will be four different cross-validation procedures, and we will use Root Mean Squared Error (RMSE) as the performance metric.


## 3. Experiment description
For now, we are concealing some details of the experiment so that challengers do not attempt to locate the full publicly-available dataset. (Note: any evidence of cheating will result in disqualification.) However, we will disclose all information at the end of the competition.

The data are from an experiment conducted in a laboratory setting. Study participants were exposed to several emotional videos (in random order) that were between approximately 2-3 minutes long. While watching each video, participants provided moment-to-moment ratings of their emotions using a joystick that traversed a two-dimensional valence (x-axis) arousal (y-axis) space (i.e., a “2D circumplex”). These ratings were sampled at 20Hz. 

Simultaneously, the following physiological signals were sampled at 1kHz:

*Cardiac activity*
- Photoplethysmography (bvp) signal was captured with a sensor placed on the middle finger of participants’ non-dominant hand.
- Electrocardiography (ecg) signal was captured using pre-gelled electrodes placed on the participants’ chests in a triangular configuration.

*Muscle activity*
- Muscle activity for the corrugator supercilii (emg_coru), trapezius (emg_trap), and zygomaticus major (emg_zygo) was captured using standard configurations of electromyography sensors.

*Electrodermal activity (gsr)*
- Variation in electrical conductance resulting from sweat released by skin glands was measured with GSR sensors placed on the index and ring fingers of participants’ non-dominant hand.

*Respiration trace (rsp)*
- Respiration was measured with a piezo-electric belt attached under the armpits and above the breasts.

*Skin Temperature (skt)*
- Variation in skin temperature was measured with an epoxy rod thermistor attached to the pinky finger of participants’ non-dominant hand. 


## 4. Data structure
All the data is stored in [releases](https://github.com/Emognition/EPiC-2023-competition/releases/latest) section of the repository in password-protected .zip files. (On the Github website, this appears to the right of this Readme text.) To extract the data you should be able to use any software supporting password-protected zip files--and we can confirm that we've been able to do so using 7-Zip, WinZip, and p7zip. The password has been emailed to all competitors.

Data are divided into four scenarios, each representing a different validation approach. Every scenario contains a train and test set with physiological measures and ground truth annotations. There is a .csv file per data sample (one subject watching one video) with the filename sub_X_vid_Y.csv where X and Y are the IDs of the participant and video, respectively. We have provided an image that [illustrates the four scenarios](https://github.com/Emognition/EPiC-2023-competition/blob/main/EPiC_Scenarios_ExplainerFigure.png), and more information is below.

1. **Across-time scenario** corresponds to the *hold-out* validation approach that respects chronology. Each sample is divided into training and test parts based on time. A sample represents a single person watching a single video. The earlier parts of the video are in the training set, and the later parts are in the test set.

	This scenario examines how well a model utilizes knowledge obtained from past data to make predictions about new data collected from the same set of participants and emotional context.



2. **Across-subject scenario** matches the *leave-N-subjects-out* validation approach. Participants are divided into random groups. All the samples of a given group of participants belong either to the train or test set, depending on the fold. There are 5 folds in this scenario, and each fold leaves out a different set of subjects.

	This scenario examines a model’s ability to generalize knowledge obtained from a group of people to a different, previously unseen, group of people.



3. **Across-elicitor scenario** follows the *leave-one-stimuli-out* validation approach. For every subject there are two samples (videos) per each quadrant in the arousal-valence space. In each fold both samples related to a given quadrant are excluded, resulting in 4 folds, each excluding one arousal-valence quadrant.

	This scenario examines how well models trained on three arousal-valence quadrants (e.g., high arousal, high positivity; high arousal, high negativity; low arousal, high positivity) can infer states experienced in the fourth quadrant (e.g., low arousal, high negativity). In other words, it examines how well a model trained on specific emotional states can generalize to a different, previously unseen, set of emotional states. 


4. **Across-version scenario** resembles the *hold-out* validation approach that doesn’t necessarily respect chronology. For every subject there are two samples (videos) per each quadrant in the arousal-valence space. In this scenario, one sample is used to train the model, and the other sample is used to test the model. Thus, this scenario has 2 folds.

	This scenario examines how well models trained on one specific instantiation of an emotional state can generalize to different inductions of that same emotional state. Similar to the first scenario, the same set of participants are used for training and testing.


### More information about the data
For each scenario, there will be both training and test data sets. Teams can further divide the training set (e.g., into training and validation) if they would like.

In the test set, the length of the physiology recordings is 20 seconds longer than the length of the self-reported emotion (ground truth). This is to allow people to build models that use time windows of up to 20 seconds long–10 seconds of physiology recordings before and and after the self-reported emotion. Please note, though, that teams can decide what architecture, which physiological signals, which features, what window size, etc. to use.

Data files in test sets have columns (arousal and valence) and timestamps defined. Your task is to predict arousal and valence levels for all of the provided timestamps. You can use the files as a template that you have to fill with predictions produced by your solution.

For a more visual explanation of how the dataset is constructed and organized, you can see the attached example notebook [explain_data.ipynb](https://github.com/Emognition/EPiC-2023-competition/blob/main/explain_data.ipynb). It shows how to load data, and what the data look like when stored in memory and plotted.


## 5. Code of Conduct
The rules governing our collaboration are in the [collaboration agreement](https://github.com/Emognition/EPiC-2023-competition/blob/main/EPiC_2023Challenge_CollaborationAgreement.pdf). By participating in the challenge, you are indicating that you agree to abide by the collaboration agreement.

Below is a summary of the basic rules of the competition:
- You are free to explore various modeling approaches. 
- You may use pretrained models and/or use other datasets to pretrain your model. If you do so, the datasets/models must be publicly available.
- You must refrain from dishonest behavior, such as manually tuning the model to overfit on the test data.
- You retain the intellectual property (IP) rights for your shared/submitted code. However, it must be made openly available and reasonably easy to reproduce.
- You must be willing to serve as a co-author on a paper describing the challenge results.

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

## 8. ACII workshop paper submission
April 28th is the deadline for both (a) completing the challenge and (b) submitting short papers to the 2023 Affective Computing + Intelligence Interaction Conference workshop. 

**If you plan on submitting a short paper, you will have to submit your Final Submission early: by end-of-day April 26**. We will then email you your results on April 27, giving you one day to add the information and submit the final paper.

Conference paper submission and formatting guidelines can be found [here](https://acii-conf.net/2023/wp-content/uploads/2023/03/2023-ACII-Submission-Guidelines.pdf).

## 9. Concluding remarks
Thank you for participating in our challenge. Now, go off and be EPiC!
