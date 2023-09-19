# LuViRA_Dataset
Lund University Vision, Radio, and Audio (LuViRA) Dataset

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


# Data Structure

The LuViRA dataset stored as:

```
dataset_directory
            └── Vision                      
                    └── Mono                 
                      └── Grid               
                      └── Random               
                    └── RGB-D 
            └── Radio            
                      └── Grid101.mat
                      └── Grid102.mat
                      └── ...           
            └── Audio     
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

                    └── raw
```

# Notes
