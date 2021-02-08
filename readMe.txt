################################### Folder Structure

Root Folder Contains two folders (model folder, data folder):-
1) codes: containin codes for EnAppX, EnAppX-F, EnAppX-SPC, EnAppX-d (dimension d), EnAppX-K (Number of Features K in FAGen)
2) Data: THS city- ths_ODT_3months.npy ; NYC Green Taxi 2014 data can be obtained online and framed the same way.


################################## Preliminary

1. Inside codes/<model> ; create folders named <output>, <output/NYC>, <output/THS>, <repo>, <res>

2. Set epochs value in trainTest() method of getRunNYC.py/getRunTHS.py

3. execute runNYC.sh/runTHS.sh {(i) set chmod for sh file. (2) type: ./runNYC.sh (./runTHS.sh)}


################################ Process of Training and Testing

1. From <output/NYC/dfStatsNYC_epochs_H.csv> (/ <output/NYC/dfStatsTHS_epochs_H.csv> ) determine where trend of training_loss and validation_loss to observe no overfitting or underfitting is occuring. Note the epoch number (#epochs) where validation_loss converges.

2. Set epochs (#epochs) value in trainTest() method of getRunNYC.py/getRunTHS.py

3. Execute runNYC.sh/runTHS.sh {(i) set chmod for sh file. (2) type: ./runNYC.sh (./runTHS.sh)}

4. predicted file in form of numpy array can be seen in <repo>

5. results can be seen in <output/NYC/resNYC.csv> (<output/THS/resTHS.sh)


################################## Environment

1. The attached (myenv.yml) file is the conda environment in which this code has been executed. 

2. OS is ubuntu. Python3

3. Some important packages are mentioned:-
    keras
    tensorflow
    hyperopt (omitted for cpu execution)
    pandas
    numpy
    random
	
    *seed for random, numpy, tensorflow, python has been set.


################################## Files Description

1. APPROX.py : this is the Shared-Private Component (SPC) of the Approximator in EnAppX model.

2. FAVARD.py : this is the FAGen module of Approximator in EnAppX model.

3. EnDe.py : It is the complete EnAppX model. It integrates all the modules of TGCN (HOGCN.py), LSTM, FAGen (FAVARD.py), SPC (APPROX.py) for the model. 

4. HOGCN.py : It is the file that implements TGCN module of EnAppX. This file contains contains a 2-D kernel weight (similar to that of a single GCN). This same kernel operates on each element of a sequence of ODMs (ODT). Thus implementing a time-distributed GCN operation.

5. getRunNYC.py (/ getRunTHS.py) : This takes numpy array of NYC (/ THS) as ODT input. It calls EnAppX model and train-validate and predict. Any tuning parameters need to be adjusted here. It creates all output files.

6. getNYC.sh (/ getTHS.sh) : This is a shell script for running getRunNYC.py (/ getRunTHS.py) along with their command line arguments for automatic execution and result storation.

**** For different <models> corresponding modification are made in these above respective files. Those minute modification can be easily observed in the appropriate place in these files.


###################################  Data

1. Dataset is taken from the respective links for NYC and THS. 
2. As described in the paper, ODT is constructed.
3. ODT is a numpy array of dimension (time X ordered_number_of_grid X ordered_number_of_grid) 
4. ODT is taken by getRunNYC.py (/ getRunTHS.py)


