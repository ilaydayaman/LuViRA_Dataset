# Introduction
The **Lund University Vision, Radio, and Audio (LuViRA)** positioning dataset consists of 89 trajectories that are recorded in the Lund University Humanities Lab's Motion Capture (Mocap) Studio using a MIR200 robot as the targeted platform. Each trajectory contains data from four different systems, vision, radio, audio and a ground truth system that can provide within 0.5mm localization accuracy. A Motion Capture (Mocap) system in the environment is used as the ground truth system, which provides 3D or 6DoF tracking of a camera, a single antenna and a speaker. These targets are mounted on top of the MIR200 robot and put in motion. 3D positions of the 11 static microphones are also provided. Since the targets are located on a fixed height on the robot, these trajectories can also naturally be reduced to 2D.

The main dataset is divided into two parts, "Grid Data" covering the measurement area with line trajectories, and "Random data" that are non-grid trajectories. The "random" trajectores are either manual, unscripted movement or programmed, smooth movement.

The dataset also provides additional data. One is an audio recording of the background noise (fans) in the environment while everything is static (thus not including any noise from the robot movement). There are also 8 "audio only" trajectories recorded, where only the audio and the ground truth systems are activated, thus reference recordings with less background noise. These recordings did not use the robot, but a human moving the speaker freely in the room. One implication is that there is intentional heigh variation, one is that the environment is inherently dynamic, as the human body may occasionally obstruct the direct path to some ground truth cameras and to some microphones.

This repository contains the data for our paper:

**The LuViRA Dataset: Measurement Description**  
Ilayda Yaman, Guoda Tian, Martin Larsson, Patrik Persson, Michiel Sandra, Alexander Dürr, Erik Tegler, Nikhil Challa, Henrik Garde, Fredrik Tufvesson, Kalle Åström, Ove Edfors, Steffen Malkowsky, Liang Liu

# Bibtex
If you find our work to be useful in your research, please consider citing our paper about the dataset:
```
@misc{yaman2023luvira,
      title={The LuViRA Dataset: Measurement Description}, 
      author={Ilayda Yaman and Guoda Tian and Martin Larsson and Patrik Persson and Michiel Sandra and Alexander Dürr and Erik Tegler and Nikhil Challa and Henrik Garde and Fredrik Tufvesson and Kalle Åström and Ove Edfors and Steffen Malkowsky and Liang Liu},
      year={2023},
      eprint={2302.05309},
      archivePrefix={arXiv},
      primaryClass={eess.SP}
}
```
For more information about the validation of the dataset, you can refer to our paper:
```
@misc{yaman2023indoor,
      title={Indoor Localization Using Radio, Vision and Audio Sensors: Real-Life Data Validation and Discussion}, 
      author={Ilayda Yaman and Guoda Tian and Erik Tegler and Patrik Persson and Nikhil Challa and Fredrik Tufvesson and Ove Edfors and Kalle Astrom and Steffen Malkowsky and Liang Liu},
      year={2023},
      eprint={2309.02961},
      archivePrefix={arXiv},
      primaryClass={eess.SP}
}
```

The radio-based localization algorithm we developed using this dataset: 
```
@INPROCEEDINGS{tian2023icc,
  author={Tian, Guoda and Yaman, Ilayda and Sandra, Michiel and Cai, Xuesong and Liu, Liang and Tufvesson, Fredrik},
  booktitle={ICC 2023 - IEEE International Conference on Communications}, 
  title={High-Precision Machine-Learning Based Indoor Localization with Massive MIMO System}, 
  year={2023},
  volume={},
  number={},
  pages={3690-3695},
  doi={10.1109/ICC45041.2023.10278664}}
```

# Description

Being a realistic dataset, there are imperfections that should be kept in mind when using it.
For detailed measurement log, please see: 

https://docs.google.com/spreadsheets/d/1Wo1emus49q3nXsXXXrSd7V33IDcYeVu4-jj-yxmDW6Y/edit?usp=sharing

This document has comments and temperature for each trajectory, as well as indicating what audio was used and the section cut out from raw files. If needed, the structured text file can be downloaded and read programmatically.

### Snapshot Rate of different systems ###
Ground truth system -> 100Hz  
Camera -> color-30fps, infra/depth-15fps, gyro-400Hz, accel-100Hz  
Wireless -> 100Hz  
Sound -> 96 kHz

### Post-processing Remarks ##

For convenience, the published data are (in most cases) not the raw recordings, but processed so the systems align in time.
Each trajectory is cut from 1 second before the movement starts to 1 second after the movement ends: [movement_start-1s : movement_end+1s]

The RGB images and depth maps are extracted from the rosbags and aligned as .png files as a part of the post-processing step.

To assist with collecting the information from various sources in the camera and performing necessary format conversion, we have created a separate script that handles the conversion automatically: https://github.com/niil87/Nik_OrbSlam. 

# Data Structure

## Grid Data/Trajectories

75 trajectories where the robot moves back and forth in a (mostly) straight line (while facing the same side of the studio). The ''Grid120" trajectory was deleted from the radio system since the synchronization was lost between the LuMaMi and UE. The files for ground truth vision and audio systems are kept for completeness.

Named as: Grid101, Grid102, ..., Grid176. 

## Random Data/Trajectories

14 trajectories were recorded with different movement patterns. Some of the trajectories involve people moving around in the effective area. 

List of the trajectories: 

1. Random_Rect1
2. Random_Rect2
3. Random_diag1
4. Random_diag2
5. Random_manual_people1
6. Random_manual_people2
7. Random_L
8. Random_U
9. Random_manual3
10. Random_manual4
11. Random_manual5
12. Random_circle1
13. Random_circle2
14. Random_manual_people6

## Additional Data

List of additional data provided with the dataset
1. "Audio only" data (with ground truth), using speech or one of two different music signals. These additional recordings and corresponding GT are available only in raw form. 
   - music0001
   - music0002
   - music0003
   - music0004
   - speech0001
   - speech0002
   - speech0003
   - speech0004

2. "Audio noise" data: Background noise in the environment 

# Storage

You can access the LuViRA dataset from:

http://download.eit.lth.se/LuViRA_dataset/

Username: download   
Password: download

Overall, the LuViRA dataset is stored as:

```
LuViRA_dataset
      └── Mono_grid.zip            # vision system - monocular (RGB or color) images, Grid trajectories
      └── Mono_random.zip          # vision system - monocular (RGB or color) images, Random trajectories
      └── RGB-D_grid.zip           # vision system - Depth maps and RGB or color images, Grid trajectories
      └── RGB-D_random.zip         # vision system - Depth maps and RGB or color images, Random trajectories
      └── Selected_rosbags.zip     # vision system - a selected number of raw files 
      └── Radio.zip                # radio system  - Grid and Random trajectories
      └── Audio_grid.zip           # audio system  - Grid trajectories
      └── Audio_random.zip         # audio system  - Random trajectories
      └── Audio_noise.zip          # audio system  - additional data, background noise
      └── Audio_only.zip           # audio system  - additional data that includes only the audio sensor
      └── Ground_truth.zip         # GT system     - processed files, time-aligned with each published sensor data
      └── Ground_truth_raw.zip     # GT system     - raw files, each marker position as output from system
```

More detailed data structure with examples from different folders: 

```
dataset_directory
      └── vision  # the name of the .png files are the true timestamps provided by the NTP server                    
            └── Mono_grid             
                  └── RealSense_D435i_mono.yaml 
                  └── Grid101
                        └── mav0/cam0/data/
                              └── data.csv 
                              └── 1651916361.263793945.png 
                              └── 1651916361.297067165.png
                              └── ...
                  └── Grid102  
                  └── ...         
            └── Mono_random               
            └── RGB-D_grid    
                  └── RealSense_D435i_rgbd.yaml             
                  └── Grid101
                        └── associations.txt
                        └── rgb
                              └── data.csv 
                              └── 1651916361.263793945.png  
                              └── 1651916361.330339432.png
                              └── ...
                        └── depth    
                              └── data.csv 
                              └── 1651916361.263793945.png  
                              └── 1651916361.330339432.png  
                              └── ...      
                  └── Grid102       
                  └── ...              
            └── RGB-D_random           
            └── Selected_rosbags  
      └── radio   # formatted as (100,100,100) -> (time, frequency, antenna)         
            └── Grid101.mat
            └── Grid102.mat
            └── ...           
      └── audio_grid   # 12 Microphones + 13th recording is the start signal from the ground truth system (Sync) 
            └── Grid101          
                  └── Sync.wav     
                  └── Track 1.wav     
                  └── Track 2.wav          
                  └── ...     
            └── Grid102        
            └── ... 
      └── audio_random   # 12 Microphones + 13th recording is the start signal from the ground truth system (Sync) 
      └── ground_truth
            └── extracted
                  └── Grid101.csv
                  └── Grid102.csv
                  └── ...
            └── raw      
                  └── 3D
                        └── Grid0101.tsv
                        └── Grid0102.tsv
                        └── ...
                  └── 6D   
                        └── Grid0101_6D.tsv
                        └── Grid0102_6D.tsv
                        └── ...
```

# Notes

1. **For the vision system:** Only a selected number of rosbag files are given. Other rosbag files can be provided on request. The files occupy approximately 900GB of space. 
2. **Format of the processed ground truth system files:** ''Rot" stands for the 3x3 rotation matrix
```
# timestamps, X, Y, Z, Roll, Pitch, Yaw, Residual, Rot[0], Rot[1], Rot[2], Rot[3], Rot[4], Rot[5], Rot[6], Rot[7], Rot[8]
```
3. **Separately tracked:** Although the camera, antenna and speaker follow the robot trajectory, do note that they are distinct objects with separate ground truth trajectories, and their orientation also does not neccesarily match the orientation of the robot (direction of travel). Being fixed on the robot, a rigid 6DoF tranformation should be able to align them however.

