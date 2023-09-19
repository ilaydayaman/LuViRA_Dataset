# Description
Lund University Vision, Radio, and Audio (LuViRA) Dataset consists of 88 trajectories that are recorded in the Lund University Humanities Lab's Motion Capture (Mocap) Studio using a MIR200 as the targeted platform for positioning. Each trajectory contains data from four different systems, vision, radio, audio and a ground truth system that can provide within 0.5mm localization accuracy. Motion Capture (Mocap) system in the environment is used as a ground truth system which provides 3D or 6DoF labels to a camera, a single antenna and a speaker. These targets are mounted on top of the MIR200 robot and put in motion. 

This repository contains the data for our paper:

**The LuViRA Dataset: Measurement Description**  
Ilayda Yaman, Guoda Tian, Martin Larsson, Patrik Persson, Michiel Sandra, Alexander Dürr, Erik Tegler, Nikhil Challa, Henrik Garde, Fredrik Tufvesson, Kalle Åström, Ove Edfors, Steffen Malkowsky, Liang Liu

# Bibtex
If you find our work to be useful in your research, please consider citing our paper:
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

75 trajectories where robot moves back and forth in a (mostly) straight line (while facing the same side of the studio). 

Named as: Grid101, Grid102, ..., Grid175

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
   - music0test
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

The LuViRA dataset stored as:

```
dataset_directory
      └── Vision  # the name of the .png files are the true timestamps provided by the NTP server                    
            └── Mono                 
                  └── Grid               
                  └── Random               
            └── RGB-D                
                  └── Color               
                  └── Depth
      └── Radio   # formatted as (100,100,100) -> (time, frequency, antenna)         
            └── Grid101.mat
            └── Grid102.mat
            └── ...           
      └── Audio   # 12 Microphones + 13th recording is the start signal from the ground truth system  
            └── Grid101            
                  └── 1            
                  └── 2          
                  └── ...     
            └── Grid102         
                  └── 1            
                  └── 2          
                  └── ...  
            └── ... 
      └── Ground truth
            └── extracted
                  └── Grid0101.csv
                  └── Grid0102.csv
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
