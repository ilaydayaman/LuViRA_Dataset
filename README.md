# Description
Lund University Vision, Radio, and Audio (LuViRA) Dataset consists of 88 trajectories that are recorded in the Lund University Humanities Lab's Motion Capture (Mocap) Studio using a MIR200 as the targeted platform for positioning. Each trajectory contains data from four different systems, vision, radio, audio and a ground truth system that can provide within 0.5mm localization accuracy. Motion Capture (Mocap) system in the environment is used as a ground truth system which provides 3D or 6DoF labels to a camera, a single antenna and a speaker. These targets are mounted on top of the MIR200 robot and put in motion. 

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

The radio based localization algorithm we developed using this dataset: 
```
@misc{tian2023highprecision,
      title={High-Precision Machine-Learning Based Indoor Localization with Massive MIMO System}, 
      author={Guoda Tian and Ilayda Yaman and Michiel Sandra and Xuesong Cai and Liang Liu and Fredrik Tufvesson},
      year={2023},
      eprint={2303.03743},
      archivePrefix={arXiv},
      primaryClass={eess.SP}
}
```

# Description

For detailed measurement log, please see: 

https://docs.google.com/spreadsheets/d/1Wo1emus49q3nXsXXXrSd7V33IDcYeVu4-jj-yxmDW6Y/edit?usp=sharing

### Snapshot Rate of different systems ###
Ground truth system -> 100Hz  
Camera -> color-30fps, infra/depth-15fps, gyro-400Hz, accel-100Hz  
Wireless -> 100Hz  
Sound -> 96 kHz

### Post-processing Remarks ##

All the data is cut from 1s before the movement starts to 1s after the movement ends: [movement_start-1s : movement_end+1s]

The RGB images and depth maps are extracted from the rosbags and aligned as .png files as a part of the post-processing step.

To assist with collecting the information from various sources in the camera and performing necessary format conversion, we have created a separate script that handles the conversion automatically: https://github.com/niil87/Nik_OrbSlam. 

# Data Structure

## Grid Data/Trajectories

75 trajectories where robot moves back and forth in a (mostly) straight line (while facing the same side of the studio). The ''Grid120" trajectory was deleted from the radio system since the syncronization was lost between the LuMaMi and UE. The files for ground truth vision and audio systems kept for completeness.

Named as: Grid101, Grid102, ..., Grid176. 

## Random Data/Trajectories

13 trajectories recorded with different movement patterns. Some of the trajectories involve people moving around in the effective area. 

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

## Extra/Additional Data

List of additional data provided with the dataset
1. Speaker only
   - music0001
   - music0002
   - music0003
   - music0004
   - speech0001
   - speech0002
   - speech0003
   - speech0004

2. Background noise in the environment 

# Storage

You can access the LuViRA dataset from:

http://download.eit.lth.se/LuViRA_dataset/

Username: download   
Password: download

Overall, the LuViRA dataset is stored as:

```
LuViRA_dataset
      └── Mono_grid.zip      # vision system
      └── Mono_random.zip    # vision system
      └── RGB-D_grid.zip     # vision system
      └── RGB-D_random.zip   # vision system
      └── Radio.zip          # radio system
      └── ground_truth.zip   # ground truth system
      └── ground_truth_raw.zip   # ground truth system
      └── audio.zip          # audio system
      └── audio_only.zip     # additional data
      └── noise.zip          # additional data
```

More detailed data stucture with examples from different folders: 

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
      └── radio   # formatted as (100,100,100) -> (time, frequency, antenna)         
            └── Grid101.mat
            └── Grid102.mat
            └── ...           
      └── audio   # 12 Microphones + 13th recording is the start signal from the ground truth system (Sync) 
            └── Grid101          
                  └── Sync.wav     
                  └── Track 1.wav     
                  └── Track 2.wav          
                  └── ...     
            └── Grid102        
            └── ... 
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
