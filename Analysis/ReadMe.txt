
#Directories will be generated if not present during the exhaustive search and then during the analysis.
root_dir : ../Lets_talk_about_svm/dataset
Input Directory: ../Lets_talk_about_svm/Results_simulations
Output Directory: ../Lets_talk_about_svm/Results and Analysis

    ###################################################################################################################################################
    A.  Simulation files to get total results i.e. plainSVRm_2024.py and plainSVRs_2024.py 
    ###################################################################################################################################################
    Path: ../Lets_talk_about_svm/
    
    Purpose: These files are used to run the final big configuration i.e., C8 to perform an exhaustive search for SVR for both Multioutput_SVR and Singleoutput_SVR

    How to execute:
    There are two methods to execute these files.
        1. Run the files directly from the Python environment as they also behave as independent files to run execution (both files: plainSVRm_2024.py and plainSVRs_2024.py)
        2. You can use runmethod_cmd.py file to execute these files as well. it is also present in the same directory.

        Commands for the first run are also added at the end of each file as a template for execution.
    
    These files will read the data from the dataset folder in the root directory, i.e., root_dir, and execute it. They will perform multiple tasks required for simulation. 
    It will keep the record of each combination in progress_file.json so that if the system crashes, it will skip the already executed files. Even if any combination form 
    the JSON file or the results from the input directory was removed mistakenly, then it will just execute the relevant combination from the previous combinations.


    ###################################################################################################################################################
    B.  Let's Talk about the Functions used in getCi_cmd.py: A command-based analysis in the analysis folder
    ###################################################################################################################################################
    
    File Path: ../Lets_talk_about_svm/Analysis/getCi_cmd.py
    Purpose: Analysis based on the given results from the Input directory and the results will be saved in the output directory.
    Command :  python getCi_cmd.py --config_name C1 C2 or any --datasets DSI2 MAN2 --subfolders plainSVRs_2024 plainSVRm_2024

    ###################################################################################################################################################
    Note:
    These are all the files used for the analysis purpose, it will take the data from the Results_simulations folder, generated using plainSVRm_2024.py and plainSVRs_2024.py 
    from the Lets_talk_about_svm folder. Using commands, these files can be executed independently or runmethod.py from the Lets_talk_about_svm folder.


    It is the file for command-based results and analysis and it will generate output in the output directory for each configuration C1 to C8 is a structure like:
    output directory/plainSVRs_2024/config_name/dataset_name/configuration_folder/error_rep*.csv and prediction_rep*.csv file

    Command description used for analysis:
            It will accept config names like C1,C2,C3, to C8 , dataset name like DSI1,DSI2 (more then one names), 
            and subfolder and generated during results and simulation i.e. (plainSVRs_2024, plainSVRm_2024)

    Functions used in getCi_cmd.py:
    1. copy_config_files()
        This function reads the input configuration's relevant combination files from the input directory and then saves the relevant files in the output directory.
        It will generate a folder structure like: output directory/plainSVRs_2024/config_name/dataset_name/configuration_folder/error_rep*.csv and prediction_rep*.csv file.
        This function is commented out in save_summary_files(), as it takes a little time to copy for a big configuration, uncomment it the first time to get the files, and then comment it again to save time.

    2. save_summary_files()
        This function generates two summary files for each given input mentioned in the command (plainSVRs_2024 plainSVRm_2024)
        1. First will save outputs i.e., Dataset name, mean error and standard deviation for given configurations like: Dataset, Mean Error, Standard Deviation
        2. It will save the values of the best configuration of the given data like:  Dataset, C, Kernel, Gamma, Epsilon, Tolerance, Mean Error, Standard Deviation

    3. process_error_files()
        This function is reading all the error files and processing them to calculate the mean error and standard deviation.

    4. find_best_configurations()
        This is the main function that is doing all the analysis and process
    

    ###################################################################################################################################################
    C.  Static file to execute directly getC1.py to getC8.py
    ###################################################################################################################################################

    If you don't want to use the command line then use getC1.py to getC8.py and or replace the value of config_name = "C1 to C8" in getC1.py, with the required configuration name, it will do the same. 
    keep in mind, also adjust the repetition number if using different repetitions.

    It can be possible that you can generate 8 files for each configuration. so that you do not have to change the value of config_name = to any config name eg "C3"

    If you want to save the files as well from the final configuration then uncomment the save_repetition_files() from save_summary_files() fuction, It is just needed once. 
    Then comment it to save time.

    ###################################################################################################################################################
    D.  Command-based file to execute independent combinations= getc1_cmd.py:  renamed as getCi_cmd.py
    ###################################################################################################################################################

    1. getc1_cmd.py

    This file is for command base execution to check the output of any individual combinations.
    To execute this, change the directory of the folder to make the command short as "python getc1_cmd.py 0.2 DSI1 1.0 rbf scale 0.001 3 0.001 0 5"   use without "". else use the long path as mentioned below
    
    How to change the directory:  
    cd "Lets_talk_about_svm/MultiOutput_SVR/Analysis/getc1_cmd.py"
    
    Then type: python getc1_cmd.py 0.2 DSI1 1.0 rbf scale 0.001 3 0.001 0 5
    
    Numbers are the parameters in a sequence used in the runmethod_cmd() function
    EG: Base Name: DSI1,  Split: 0.2, C: 1.0, Kernel: rbf, Gamma: scale, Epsilon: 0.001, Tol: 0.001, Repetitions: 5


    ###################################################################################################################################################
    E.   getCi_master_copy.py 
    ###################################################################################################################################################
    It is the master copy for the static files.
    In this file, I am doing the analysis of the individually given combination so that I can get the output analysis for the given configuration only



    ###################################################################################################################################################
    F.   Let's talk about helping files that contain the helping function
    ###################################################################################################################################################

    helping_functions_svm.py
        It has multiple functions required to execute the main files i.e. plainSVRm_2024.py and plainSVRs_2024.py
        Functions: fit_and_evaluate_model, prepare_data, save_results, save_progress, load_progress, files_exist, generate_param_combinations
    
    processing.py
        This file contains the processing function required to process the data.
        Functions: min max scaler, process_datasets

    optimization_function.py
        I am not using this file yet, However, it contains some optimization functions.


    ###################################################################################################################################################
    G.   Lets talk about: getBestParams_cmd_individual.py
    ###################################################################################################################################################

    Command: python getBestParams_cmd_individual.py -fold plainSVRm_2024 -ts 0.2 -DS DSI2 -C 1.0 -K rbf -g scale -e 0.001 -d 3 -t 0.001 -coe 0.0 -rep 2


    ###################################################################################################################################################
    H.   Lets talk about JSON, log and PKL files
    ###################################################################################################################################################
    progress_file.json
        It is the JSON file that contains the progress of the models. It records each processed combination during an exhaustive search. It will help us track the  combinations
    so that when the system crashes or is interrupted etc, then we can resume from the last recorded combination while skipping the previous combinations.
    
    config.json:
    It is the JSON file that contains the configuration of the system. I just recording the final configuration here. But I am not using it.

    svr_run_log
        This file records the logs or the errors of the executions.

    progress_pkl
        It is the same as progress_file.json, but I am not using it.
