# Diagnosis and Causal Analysis of Depression Based on EEG Features and Machine Learning


####   Lizhuo Shao, Lanqi Li, Qianke Du, Jiayi Wang, Yupu Chen, Ningbo Yu*  #########
####   Department of  Artificial Intelligence                               #########
####   Nankai University                                                    #########
####    2111078@mail.nankai.edu.cn                                           #########


## Abstract
对EEG脑电信号与抑郁症关系的因果分析
## I.  INTRODUCTION
  In this study, we used electroencephalogram (EEG) data to extract the features of EEG alpha interhemispheric asymmetry, activity, and mobility, combined with machine learning algorithms, to explore the effective features for the diagnosis of depression, and revealed the relationship between these features and depression through causal analysis. Through the prediction and analysis of machine learning methods such as SVM, Random Forest and XGBoost, we found that Xgboost performs most consistently in processing these features. The results showed that prefrontal asymmetry (Fp1-Fp2), parietal lobe asymmetry (P3-P4),occipital lobe asymmetry (O1-O2) , and temporal lobe asymmetry (T5-T6) were the key features affecting the diagnosis of depression. Further causal analysis showed a direct causal relationship between prefrontal asymmetry and parietal lobe asymmetry and depression.

## II.  DATA PROCESSING 
### A.	Data Set Acquisition
  The data set of depressed patients used in this study was obtained from the outpatient clinic of hospital Universiti Sains Malaysia (HUSM) and was a public data set. It included a total of 33 patients with depression with a mean age of 40.33 and 30 healthy subjects as control group with a mean age of 38.23.
### B.	Experimental data collection
  EEG data were recorded for 5 minutes with eyes closed and 5 minutes with eyes open, involving a 19-channel EEG cap with linked-ear(LE)reference.EEG sensors were placed on the scalp according to the international 10-20 electrode placement standard.The 19-electrodes covering the scalp included the frontal  (Fp1, Fp2, F3, F4, F7, F8, Fpz), parietal (P3, P4, P7, P8) , occipital (O1, O2),temporal (T3, T4, T5, T6),and the central area (C3, C4) regions. 
### C.	EEG signal data preprocessing
The EEG signals in the dataset were first subjected to independent component analysis (ICA) to separate the multidimensional mixed signals .
![image](https://github.com/LQ-sama/Causal_ML_For_EEG/assets/132965726/4ec0bbb8-d1a0-4e37-89f9-f7a4559bea16)

Fig. 1 Raw EEG data after noise removal

![image](https://github.com/LQ-sama/Causal_ML_For_EEG/assets/132965726/700f401f-9420-4e7d-9cac-0c9a679f8bb4)

Fig. 2 EEG data after independent component analysis

## III.  FEATURE EXTRACTION
Considering that experimenters might not have been in 
the state at the beginning and end of the experiment, the first and last 30 seconds of each were discarded.
	Considering the small amount of data, we intercepted a segment of valid data every T time period and extracted its asymmetric features. After repeated experiments, it was determined that taking T as 45 (second) had the best effect.
![image](https://github.com/LQ-sama/Causal_ML_For_EEG/assets/132965726/1df53ee2-31f4-4bf6-831c-251e306e85df)

### A.	EEG alpha interhemispheric asymmetry
Differences in observations such as the power of the EEG signal between the left and right hemispheres could be observed and calculated using quantities such as interhemispheric asymmetry[10]. Equation (1) and (2) described the mathematical formulas for calculating power in the desired frequency bands.

Where the upper and lower frequencies for band-limited EEG signal power computation are denoted by f1 and f2, respectively. The power spectral densities were denoted as SLmn and SRmn such as they represent the right and left brain hemispheres, respectively. Finally, (3) gives the formula for calculating the interhemispheric EEG asymmetry 

EEG alpha interhemispheric asymmetry was calculated for each channel pair including frontal (Fp1, Fp2, F3, F4, F7, F8, Fpz), parietal (P3, P4, P7, P8), occipital (O1, O2), temporal (T3, T4, T5, T6) and central (C3, C4).  For example, calculating the EEG alpha asymmetry for Fp1 included channel pairs such as Fp1-fp2; Fp1-F4; Fp1-F8; Fp1-T4; Fp1-T6; Fp1-P4; Fp1-P8; Fp1-02:Fp1-C4. 
### B.	Activity

Activity and mobility could be used to examine the degree of signal oscillation and were important indicators for quantitatively assessing nonstationary EEG signals.

Where y(t) denotes the EEG signal, μ is the mean value of the signal, N is the sample size of the EEG data segments, and var denotes the variance. Several EEG signal segments were selected from depressed patients and normal controls respectively during the valid time, and the activity of 22 EEG feature signals was calculated using (4).

### C.	Mobility

Where y(t) is the input EEG signal and var denotes variance. For depressed patients and normal controls respectively, several EEG signal segments were selected during the effective time, and the mobility of 22 EEG feature signals was calculated using (5).

## IV.  MACHINE LEARNING OUTCOME PREDICTION AND FEATURE IMPORTANCE ANALYSIS 
### A.	Model Predictions
![image](https://github.com/LQ-sama/Causal_ML_For_EEG/assets/132965726/5da27f23-1e5f-47f5-bb28-a44ee7ec47d8)
Machine learning model predicted results
According to the analysis of the above results, it could be seen that from the perspective of characteristic, the effect of frequency band asymmetry was better than that of mobility and activity. Moreover, alpha asymmetry and beta asymmetry were slightly more effective than theta asymmetry. From the perspective of machine learning methods, they could all achieve good results, but XGBoost and SVM had better classification effects, among which XGBoost could reach 99% classification accuracy for alpha asymmetry.	
### B.	Feature Importance Analysis
Random Forest and XGBoost were used separately to look at the importance of 64 pairs of features, aiming to assess the importance of these features in predicting the target variable related to alpha asymmetry, namely whether or not to be depressed. Through feature importance analysis, we could identify the features that had the greatest impact on the prediction results. It was calculated 1000 times and averaged, and the results were shown in Fig.10.

![image](https://github.com/LQ-sama/Causal_ML_For_EEG/assets/132965726/9f6eedc0-e198-4b44-8163-a2e423276215)

View of alpha asymmetry feature importance

The horizontal axis represents the 64 features and the vertical axis represents the weight of importance of the features (0 ~ 1) . It can be observed that the two most important features of alpha asymmetry obtained by Random Forest are prefrontal asymmetry (Fp1-Fp2) and temporal asymmetry (T5-T6); However, the two most important features obtained by XGBoost are occipital asymmetry (O1-O2), parietal asymmetry (P3-P4). Among them, the asymmetry of prefrontal EEG has been shown to be associated with depression [14]. Parietal asymmetry is related to cognitive function, and impaired cognitive function may lead to increased perception of depression [15]. Temporal lobe is related to emotion regulation and memory function [16], and occipital lobe is mainly related to visual processing [17]. The electrode distribution of the four important features mentioned above is shown in Fig.11.

![image](https://github.com/LQ-sama/Causal_ML_For_EEG/assets/132965726/5f85c259-c565-47bd-86f6-a19959c8ca2e)

 Electrode distribution of four distinct features

## V.  CAUSAL ANALYSIS
### A.	PC algorithm
We extracted the features of the four electrode pairs Fp1-Fp2, P3-P4, O1-O2, T5-T6, and merged them with the label of "whether depressed or not" to form a feature matrix with several rows and five columns. x1,x2,x3,x4,x5 were used to refer to the above five columns of data respectively, and the causal diagram was calculated by PC algorithm, as shown in Fig.12.

![image](https://github.com/LQ-sama/Causal_ML_For_EEG/assets/132965726/06796dbf-98ff-4be3-adda-b4674278ee23)

The arrow points from cause to effect. It can be seen from the Fig.12 that the PC model shows that Fp1-Fp2, T5-T6, P3-P4 have a direct relationship with depression, while O1-O2 does not have a direct relationship.

### B.	GES algorithm
To verify the reliability of the results, we subsequently used the score-based GES algorithm (GES with the BIC score or generalized score), and the calculated causality diagram was shown in Fig.13.

![image](https://github.com/LQ-sama/Causal_ML_For_EEG/assets/132965726/13135d04-0456-4a76-b8b7-ef07d5dde85a)

According to the graph, we can see that the variable x5 (depression or not) is directly affected by the three features x1 (Fp1-Fp2), x2(P3-P4), x3 (O1-O2). This indicates that there is a direct causal relationship between these three characteristics and whether or not one is depressed. Although there is no direct causal relationship between the variable x4(T5-T6) and depression, it indirectly affects depression by affecting the other three characteristics.

### C.	ICA-based LiNGAM algorithm
We then used the ICA-based LiNGAM algorithm to quantify the above causal relationship and used the resulting coefficient matrix for calculation.

![image](https://github.com/LQ-sama/Causal_ML_For_EEG/assets/132965726/dcfd0744-d7a7-4ee0-b3ef-5366bc750991)

## VI.  DISCUSSION AND CONCLUSIONS

Based on the above analysis, we can draw the following conclusions: prefrontal asymmetry (Fp1-Fp2) and parietal asymmetry (P3-P4) have a relatively obvious direct impact on whether or not one is depressed, especially prefrontal asymmetry. Temporal asymmetry (T5-T6) and occipital asymmetry (O1-O2) also have certain effect on depression, but the effect is indirect and small.
	Through the above research,we find the two most direct features that affect depression: prefrontal asymmetry (Fp1-Fp2) and parietal asymmetry (P3-P4). By combining electroencephalogram (EEG) data and machine learning algorithms, this study has proposed a more objective and accurate diagnostic method for depression. By identifying key EEG features that affect depression, it helps to improve diagnostic accuracy and reduce the reliance on subjective judgment, thus making the diagnosis more objective and reliable. Meanwhile, the monitoring of key features helps to detect depressive tendencies at an early stage, realizing early diagnosis, precise treatment and effective prevention of depression, which helps to deepen the understanding of the neurobiological mechanisms of depression and provides an important reference for future research and treatment development.

