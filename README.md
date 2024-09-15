# EEG-fNIRS bimodal emotion database

Related works: Heterogeneous Graph Convolutional Neural Networks for EEG-fNIRS Bimodal Emotion Recognition

Affective Information Processing Lab (AIPL) : https://aip.seu.edu.cn/
> The complementary spatiotemporal characteristics of electroencephalography (EEG) and functional near-infrared spectroscopy (fNIRS), their simultaneous measurement capability, and portability offer significant research potential for emotion recognition. However, limited data availability hampers progress in this field. Data collection poses privacy concerns, complicating database creation with stringent procedural standards. Moreover, due to the distinct mechanisms of EEG and fNIRS, designing appropriate equipment and synchronization paradigms is crucial. The scarcity and limitations of existing public EEG-fNIRS bimodal emotion databases highlight the need to establish a comprehensive EEG-fNIRS bimodal emotion database.

## Subject information

A total of 25 participants were recruited for this experiment, of which data from 8 participants were deemed invalid, resulting in 17 participants being selected for the final analysis. All 17 participants were students from Southeast University, aged between 21 and 26 years. They were all right-handed, with normal or corrected-to-normal vision, and had no physical or mental illnesses, color blindness, or color weakness. Additionally, none of the participants were using psychoactive medications (such as stimulants, antidepressants, or anxiolytics). Prior to the experiment, all participants were informed about the harmlessness of the experimental equipment and provided written informed consent.

## Experimental environment and equipment

During the experiment, participants were placed in a soundproof, dimly lit, enclosed environment to prevent external interference. The room temperature was maintained between 23-25°C to ensure the participants' comfort throughout the experiment. Participants sat upright in a comfortable chair approximately 70 cm away from the screen and were instructed to remain calm, keep their muscles relaxed, and avoid frequent blinking during the experiment.

To achieve synchronized acquisition of EEG and fNIRS signals, this experiment used a specially designed EEG-fNIRS dual-modality electrode cap. This cap was based on the Quik-Cap 64-channel EEG cap, which conforms to the international 10-20 system, and was modified to include slots for inserting fNIRS optodes, with EEG electrodes and fNIRS optodes arranged in an alternating pattern. At the start and end of each trial, signals were sent to the EEG and fNIRS receiving devices to mark the sample points corresponding to the beginning and end of the experiment.

* EEG signal acquisition was conducted using a 64-channel EEG system produced by Neuroscan. Stimuli were presented using the Presentation software, and signals were collected through the electrode cap. These signals were then amplified using the Synamps2 amplifier and recorded by Scan 4.5 software. Electrooculographic (EOG) signals and mastoid reference electrodes were excluded. The sampling rate during the data collection process was set at 1000 Hz, and the impedance of all electrodes was kept at 10 kΩ or below. The electrode positions used in the experiment are shown in the figure below: 

  <div align=center>
    <img src="https://github.com/TAo-200010/AiplSeu-EEG-fNIRS-emotion/blob/main/EEG_channel.png" width="300" />
  </div>
  
* The fNIRS signal acquisition was conducted using the LABNIRS near-infrared brain imaging system produced by Shimadzu Corporation. This system simultaneously measures the attenuation rates of near-infrared light at three different wavelengths—780 nm, 805 nm, and 830 nm—in the brain. These attenuation rates are then converted to oxyhemoglobin (HbO) and deoxyhemoglobin (HbR) concentrations using the Modified Lambert-Beer Law. Due to the limited number of optodes, it is not possible to cover the entire brain with electrode signals. To maximize the measurement of brain activity related to the participants' emotional states, the optodes were concentrated in the frontal, prefrontal, and bilateral temporal regions. The specific positions of the optodes and channels are shown in the figure below:

  <div align=center>
    <img src="https://github.com/TAo-200010/AiplSeu-EEG-fNIRS-emotion/blob/main/fNIRS_channel.png" width="380" />
  </div>
  
## Stimuli materials

Since all participants were Chinese students, a set of film clips from the Chinese Affective Video System was selected. These clips included 3 types of emotions: happiness, neutrality, and sadness, with 5 clips for each emotion. To ensure that participants could better understand the films and thus more effectively elicit emotions, the following two principles were followed when selecting the clips: (1) The duration of each clip should neither be too long nor too short. Clips that are too short may not sufficiently evoke emotions, while clips that are too long could cause fatigue; therefore, the duration was set to approximately 1-2 minutes; (2) Each clip should convey only one type of emotion. A total of 15 clips were chosen based on a group voting process. The detailed information for these film clips is shown in the table below:

|  ID  |        Video name         | Emotion label |
| :--: | :-----------------------: | :-----------: |
|  1   |       A Big Potato        |   Happiness   |
|  2   | The Eagle Shooting Heroes |   Happiness   |
|  3   |         Hands Up!         |   Happiness   |
|  4   |     Flirting Scholar      |   Happiness   |
|  5   |    Eat Hot Tofu Slowly    |   Happiness   |
|  6   | The IDE interface repair  |    Neutral    |
|  7   |        IP package         |    Neutral    |
|  8   |    Projection machine     |    Neutral    |
|  9   |    Repair the computer    |    Neutral    |
|  10  |     Hardware conflict     |    Neutral    |
|  11  |        Rob-B-Hood         |    Sadness    |
|  12  |        The Lovers         |    Sadness    |
|  13  |        My Beloved         |    Sadness    |
|  14  |        Warm Spring        |    Sadness    |
|  15  |    Roots and Branches     |    Sadness    |

## Experimental paradigm

The experimental protocol is depicted in the figure below:

<div align=center>
  <img src="https://github.com/TAo-200010/AiplSeu-EEG-fNIRS-emotion/blob/main/experimental%20protocol.png" width="430" />
</div>
  
Each subject completed a total of 15 trials, where each trial contained three periods, i.e., a 5-second hint period, a 1 to 2 minutes of video watching period, and a 30-second rest period. The purpose of the 30-second rest period was to allow the subject’s emotional state to return to baseline. Among the three periods of each trial, only the neural signals corresponding to the video watching period were used for the emotion recognition task.

## Preprocessing

**For EEG:**

* Re-reference: average reference method (does not require additional electrodes to record the reference potential).
* Filter: a band-pass filter of 0.3-75 Hz, followed by a 50 Hz notch filter (characteristic frequency range of EEG is primarily concentrated between 1 and 50 Hz.).
* Downsampling: 128 Hz (reduce subsequent computational costs).

* Artifact removal: ADJUST toolbox of the EEGLAB (independent component analysis automatically removes artifacts.).
* Segmentation and baseline correction. The task-related EEG signals were segmented based on the start times of the 15 video clips. Baseline correction was performed using the data from 1 second before the start of each task as the baseline.

**For fNIRS:**

* Filter: a band-pass filter of 0.01- 0.1 Hz (fNIRS signals can be affected by system noise and physiological noise).
* Segmentation and baseline correction. The task-related fNIRS signals were segmented based on the start times of the 15 video clips. Baseline correction was performed using the data from 5 seconds prior to the start of each task as the baseline.

## Database files

`EEGdata/`: The raw EEG signals.

`Nirsdata/`: The raw fNIRS signals.

`pre_eeg/`: The preprocessed EEG signals.

`pre_fNIRS/`: The preprocessed fNIRS signals.

`features_EEG_1s/`: 1s EEG differential entropy features.

`features_EEG_10s/`: 10s EEG differential entropy features.

`features_fNIRS_10s/`: 10s fNIRS hemoglobin features.

`preprocessing.m`: data preprocessing code.

`label.mat`: 0-Happiness, 1-Neutral, 2-Sadness.

**Note:** 

To conduct the emotion recognition experiments, the five-fold cross-validation strategy is adopted in the our works. Specifically, in the five-fold cross-validation experiment, each subject’s data is divided into five groups in a fixed manner. Each group contains physiological data corresponding to three movie clips inducing happy, neutral and sad emotions. During the experiment, one group is selected as the test data, while the remaining groups are used as training data. This process is repeated five times, ensuring each group serves as test data once. The average of these five rounds’ results is taken as the emotion classification accuracy for that participant. Finally, the average classification accuracy and standard deviation across all 17 participants are used as performance metrics for the model.
