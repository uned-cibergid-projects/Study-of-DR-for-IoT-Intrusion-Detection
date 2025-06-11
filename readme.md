**Code for: A Comparative Study of Dimensionality Reduction Techniques for Intrusion Detection in IoT Networks**

_Preliminary considerations_

First of all it is necessary to have the Jupyter Notebook package installed to run the programs. You may need common Python libraries, namely:  sklearn, pandas, numpy, matplotlib, genetic_selection and pickle.

Utilised Edge-IIoTset and CICIoT2023 datasets are not among the attached data in this repository. To run the programs, it is necessary to previously download the **Edge-IIoTset** and **CICIoT2023** datasets from their original sources. You can use the following links:

- Edge-IIoTset (download 'DNN-EdgeIIoT-dataset.csv'): https://www.kaggle.com/datasets/mohamedamineferrag/edgeiiotset-cyber-security-dataset-of-iot-iiot
- CICIoT2023: https://www.kaggle.com/datasets/akashdogra/cic-iot-2023

Note that the CICIoT2023 dataset is distributed as 169 separate .csv files rather than a single file. For this reason, an script is included to merge them into one.


_Overall description_

This repository contains the code used to perform the experiments described in the paper 'A Comparative Study of Dimensionality Reduction Techniques for Intrusion Detection in IoT Networks', using two benchmark datasets developed specifically for IoT intrusion detection, namely Edge-IIoTset and CICIoT2023.

The purpose of the experiments is to compare several dimensionality reduction techniques for building efficient Random Forest models. The main goal was to assess the efficiency of each model, rather than its predictive capacity alone. To this end, inference time and size of each resulting model are also reported. The Random Forest technique has been considered since it constitutes a standard in Machine Learning literature due to their flexibility, strong classification performance, inherent interpretability and minimal parameter tuning, making it easy to implement for practitioners working in real-world environments.

_Materials and Methods_

For each dataset, the experiments involve an exhaustive evaluation of each dimensionality reduction method (Chi-Squared Test, Mutual Information, Permutation Feature Importance, and Principal Component Analysis) using a sequential forward selection strategy: at each step, one additional feature (or principal component), selected according to the corresponding ranking, was added to the Random Forest model, and the resulting model was evaluated in terms of accuracy, model size, and inference time on the test set. In parallel, a Genetic Algorithm was used to identify the subset of features that maximizes accuracy. The considered methods were selected to provide a representative cross-section of the most commonly employed approaches in the feature selection literature. After this process, the best model obtained by each technique was further evaluated in terms of precision, recall, and F1-score.

The train and assessment process was carried out using a hold-out validation approach, where each dataset was split into separate training and testing sets. The models were trained on the training set, and performance metrics were computed on the independent test set to assess generalization capability. The same train-test split was used across all experiments to ensure a fair comparison between methods.


_Dataset description_

The Edge-IIoT dataset includes data collected from over 10 types of IoT and IIoT devices, including temperature, humidity, water level, pulse, flame, and pH sensors, among others. It provides a comprehensive IoT traffic setting, containing 14 types of different attacks and including a total of 61 selected features describing various aspects of the network.

On the other hand, the CICIoT2023 dataset contains network traffic captured in a testbed composed of 105 real IoT devices, including a variety of brands and types, providing an accurate representation of a real-world deployment in a smart home environment. Of particular relevance is the use of IoT devices as malicious agents, reflecting realistic internal threat scenarios where infected nodes can initiate attacks against other IoT devices. In addition to benign traffic, the dataset includes a total of 33 distinct attack types, grouped into seven main categories: Denial of Service (DoS), Distributed Denial of Service (DDoS), brute force, spoofing, reconnaissance, web-based attacks, and Mirai-related attacks. The main challenge when working with the CICIoT2023 dataset is its massive size, containing over 46 million records and 47 features per instance, including the label feature that identifies the type of attack.


_Usage_

In order to reproduce the experiments described in the manuscript, for each dataset, follow the instructions below:

        1. Download the datasets and add it to the corresponding -EdgeIIoTset or CICIoT2023- folder. For the CICIoT2023, run the 'Merge' script, for merging all separated files into a single one. 
        
        2. Run the 'preprocessing' files to perform the data preparation steps described in Section 2.4 of the paper. These include removing unnecessary columns (e.g. IP adresses), constant columns, encoding categorical features,handling duplicates and missing values, detecting and removing identical columns and data scaling. 

        3. Run the 'FS_comparison' scripts to perform the experiments related to Chi-Squared test, Mutual Information, Permutation Feature Importance and Principal Component Analysis techniques.

        4. Run the 'Genetic_Alg' scripts to to perform the experiments related to the Genetic Algorithm method for feature selection. 

- Due to storage limitations, the final models used for deployment on the Raspberry Pi device are available at the following links:

        - Edge_IIoTset: https://unedo365-my.sharepoint.com/:u:/g/personal/jc_garcia_scc_uned_es/EZiUdfoedatJtoLo8UYNumEBm74Inw1ueEvJ65bkiKNQjQ?e=KpK4zi
        - CICIoT2023: https://unedo365-my.sharepoint.com/:u:/g/personal/jc_garcia_scc_uned_es/Ec3SrYPCubRBt0c91xEeEiIBX7jhpPc7p0ZztjihyXmLBA

_Limitations_

The measurement of inference time is not exact: small variations may occur between runs. To mitigate this problem, the evaluation of each model has been repeated 10 times and the median time value has been recorded However, across multiple executions, these minor fluctuations have not been found to significantly affect the reported results.


_References_

Ferrag, M. A., Friha, O., Hamouda, D., Maglaras, L., & Janicke, H. (2022). Edge-IIoTset: A new comprehensive realistic cyber security dataset of IoT and IIoT applications for centralized and federated learning. IEEe Access, 10, 40281-40306. DOI: 10.1109/ACCESS.2022.3165809

Neto, E. C. P., Dadkhah, S., Ferreira, R., Zohourian, A., Lu, R., & Ghorbani, A. A. (2023). CICIoT2023: A real-time dataset and benchmark for large-scale attacks in IoT environment. Sensors, 23(13), 5941. DOI: 10.3390/s23135941
