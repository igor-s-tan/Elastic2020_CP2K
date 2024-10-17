# ELASTIC2020 INTERFACED WITH CP2K
## Requirements
   - the `.xyz` file with cartesian coordinates with accuracy of 10 digits at least.
   - the cp2k input file with cell parameters. They should be specified in two lines and also have the accuracy as high as possible.
     
     ```
        ABC  3.635882 3.635882 3.635882
        ALPHA_BETA_GAMMA 90.00000000 90.00000000 90.00000000
     ```
     If you want to calculate elastic constants using total stress tensor, then you should turn on its calculation in the `$FORCE_EVAL` section of the cp2k input and dump it into the file named "stress".
     
     ```
     STRESS_TENSOR ANALYTICAL
     &PRINT
       &STRESS_TENSOR ON
         FILENAME=stress
       &END STRESS_TENSOR
     &END PRINT
     ```
## Usage
 1. Run ElaStic_Setup
    
    ```bash
        python ElaStic_Setup
    ```
    choose the CP2K method and write the path to the `.xyz` file
    then follow the setup instructions as usual. Make sure that the crystal system is correctly identified.
 2. Make the calculations. Every output file should have the same name as the input file with the `.out` extension.
 3. Run ElaStic_Analyze

    ```bash
        python ElaStic_Analyze
    ```
    The script will print the list of all systems for which the geometry optimization has failed. And you should recalculate all of them. The graphs of the CV error will be saved in the Stress-vs-Strain folder.

 4. Choose the eta_max strain and the corresponding order of polynomial fit and modify the file `ElaStic_*.in`
 5. Run ElaStic_Result

    ```bash
        python ElaStic_Result
    ```
    the elastic constants will be written in the `ElaStic_*.out` file
