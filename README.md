# BroadBand data clustering and bootstraping
In this project, the broadband acoustics data is clustered by KM, AC and other algorithms and methods. 
The aim is to find a suitable clustering number of species of the scene.


Specifically, this code is to obtain the reflectances of possible species (unsupervised clusters) in the broadband acoustic dataset. 

Note that both test data and the larger data will be used to see which one is more resonable to biologists.

For details about the project and tasks, 
please contact: Mette DalGaard Agersted (mette.dalgaard.agersted@hi.no) & Yi Liu (yi.liu@hi.no)

### 1. The experimental settings & input:
+ Experimental data
  1. The test dataset (better quality, correct me if I'm wrong)
  2. The large survey data
+ Data clearning
  1. Drop irrelevant items (time/depth,Alo, Ath, PingNo, Range, etc.)
  2. Choose frequencies from 54 to 78 kHz (excluding the lowest frequencies for something 'strange' with the data)
  3. Discard no-value samples for "not a number" Nan in this case
  4. Discard samples that record either too week reflectance (noisy) or too strong (seabed for example that's irrelavent)
+ Preprocessing - Dimension reduction
  1. PCA - for visualization purposes
  2. Original - for clustering (see earlier work that shows KM and AC are capable of handling this high dimensionality)
+ Using algorithms (KM & AC):
  1. *__K-Means__
  1. AP (Affiliation Propagation) (**not scalable**)
  2. AAP (Ajusted Affiliation Propagation) (**not scalable**)
  3. Spectral Clustering (**not scalable**)
  4. Mean-Shift  (**not scalable**)
  5. *__Agglomerative Clustering__
  6. DBSCAN
  7. HDBSCAN
  
### 2. Progresses
#### 2.1 Spotted KM and AC algorithms out of the seven clustering methods and proceed with experiments on 
+ Test data - KM
+ Test data - AC
+ Survey data - KM
+ Survey data - AC

#### 2.2 PCA is not 'very' necessary for better clustering 
- PCA helps improve the clustered results, though not significantly
- PCA components help a lot in visualizing the distinguishing capability of a clustering method

#### 2.3 AC outperforms KM
- Idea - Clustering with the original data & visualizing in component space (transformed from original space)
- AC outperforms significantly KM in 
  1. more resonable clusters when scattered in pca space
  2. more resonable boundaries among clusters
  3. more robust result [always the same clustered results with random sampling repetations]

#### 2.4 Elbow algorithm suggest optimal cluster numbers [4, 8]
More specifically,
- raging cluster number from 4-8, similar results are obtained with more detailed targets spotted
- one anomaly target/cluster spotted with most samples locate at the same point

### 3. Experiment output
For each group above in **2**, **cluster numbers** are suggested to be **[4, 10]** by the Elbow method.  

Among the considered clustering algorithms, we observed that AC algorithm performs the best with both the test and site dataset, which are consistent. Based on these results, we obtain the reflectances of frequency of the clusters. 

### 4. Dataset Info.
Here's two differnt data files containing information on target strength at different frequencies for single targets.

- Each row is one target. All the columns names something like "F_.." are different frequencies and the corresponding values at a given frequency is the target strength for a given target at that given frequency.

- There are also columns including date, pingNo, Range (distance of target from the transducer), position in the beam (Alo and Ath) and depth. Depth is the last column after all the frequencies are listed. 


- When running the PCA (or AP) just use data from **54 to 78 kHz** (excluding the lowest frequencies as there is something strange with the data here).

- Note that the **first column** just contains running numbers and does not have a header.
