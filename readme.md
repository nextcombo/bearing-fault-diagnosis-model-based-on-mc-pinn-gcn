# Bearing Fault Diagnosis Model Based on MC-PINN-GCN

Preface\t    Traditional deep learning fault diagnosis methods often possess strong representation capabilities, yet they are prone to the following issues: (1) The relationships between physical indicators are overlooked: 13 indicators are often directly consolidated into a one-dimensional vector, failing to explicitly utilize the deterministic or engineering correlations among RMS, variance, peak factor, etc. (2) The physical meaning of the graph structure is unclear: Traditional GCN often uses a correlation adjacency matrix, where statistical correlations, engineering mechanisms, and mathematical identities are conflated. (3) The "PINN + classifier" approach can easily become overly formal: Directly applying a so-called "physical regularizer" to the classification logits does not guarantee that the network truly satisfies continuous dynamics. (4) The existence of residual shortcuts in free dynamics networks: If any MLP is used to fit the excitation term, it may merely replicate the target derivative, thus achieving very small residuals without reproducing the true mechanism. (5) Insufficient interpretable evidence: Attention weights can only indicate what the model focuses on, but they cannot answer why this failure is established in terms of mechanical mechanisms. To this end, we propose a mechanism-consistent physics-informed neural network for rotating machinery, especially rolling bearing fault diagnosis tasks: MC-PINN-GCN (Mechanism-Consistent Physics-Informed Neural Network–Graph Convolutional Network). The model no longer views fault diagnosis as a black box mapping of "input features—output categories," but instead models two complementary types of evidence: data-driven evidence: consisting of a relational graph formed by 13 physical statistical indicators, learning deterministic relationships, engineering mechanisms relationships, statistical relationships, and constrained learning relationships among the indicators through multi-relation GCN;
Physical Mechanism Evidence: Drive a continuous state PINN with the original vibration signal, time, rotational speed, and bearing geometry parameters to construct a differentiable dynamics residual. Use the bearing characteristic frequency subspace to assess the interpretability of different fault mechanisms on vibration responses.
Ultimately, the model will fuse the two types of evidence in a controlled manner at the classification layer.
● Dataset: CWRU West Reserve University Bearing Dataset
1. Model Overview\t1.1 Overall Architecture of the Model\tMC-PINN-GCN consists of four core components:
(1) Multi-relational Indicator Graph Encoder (Multi-relational Indicator Graph Encoder)
(2) Continuous Vibration State PINN (Continuous-State PINN)
(3) Characteristic-Frequency Library + Differentiable Ridge Projection
(4) Gradient-Isolated Physics—Data Fusion Classifier (Gradient-Isolated Physics–Data Fusion).
\t  
1.2 Innovations of the Model
Innovation 1: Multi-relational Physical Metric GCN
The conventional GCN often only has a single adjacency matrix, whereas the MC-PINN-GCN decomposes relationships into four parts: Law Edge, Mechanism Edge, Statistical Edge, and Adaptive Edge. These correspond to:
- Law Edge: Physical identities;
- Mechanism Edge: Engineering mechanisms;
- Statistical Edge: Training data statistics;
- Adaptive Edge: Network-learned supplementary relationships.
This allows the model to distinguish between "mathematical definition relationships," "engineering experience relationships," and "data-related relationships," enhancing the interpretability and invertibility of the graph structure.
Innovation Point 2: PINN does not predict categories but predicts continuous vibration states. The MC-PINN-GCN clearly distinguishes between "continuous physical states" and "discrete classification outputs." The PINN branch does not directly predict categories, but rather constructs a continuous equivalent displacement field from the raw vibration signal. The physical constraints act on the clearly mechanically meaningful continuous states, rather than on the classification probabilities or logits without physical units.
4. Innovation Point: Dual Optimizer and Dual Path Loss Design
\tMC-PINN-GCN explicitly divides the training parameters into two groups:
\t  
During training, separate classification and physical optimizers are used to ensure that the two optimization paths are clearly auditable from an engineering perspective.
2 Experimental Design
2.1 Import Data
Refer to the previous article for preprocessing of fault classification 10, and the Case Western Reserve University bearing data set: Classification 10 dataset.
\ttrain_set, val_set, test_set are all divided into training set, validation set and test set according to the ratio of 7:2:1, and finally save the data.
2.2 Feature Extraction and Graph Structure Data Generation
\tPreprocessing:
\tModel Input:
3. Fault Diagnosis Model Based on MC-PINN-GCN
\t3.1 Define the network model
3.2 Set parameters, train the model
50 epochs, accuracy 100%, the MC-PINN-GCN network significantly improves classification performance from fault signal features. It can extract important features for model recognition from fault signals, with noticeable results!
3.2 Model Evaluation
(1) Accuracy, Precision, Recall, F1 Score
(2) Fault 10 Classification Confusion Matrix
(3) Classification Label Visualization
(4) t-SNE feature visualization after model training:
3.3 Explanability Analysis
(1) Global Node Attention
Represents the attention weights of 13 physical indicators in the graph level pooling stage for a test sample, and node attention analysis reveals a clear class-specific indicator selection pattern. On a global scale, average, spectral flatness, DFA, and variance received the highest attention weights, indicating that statistical magnitude features and frequency/complexity related descriptors have significant contributions to fault discrimination.
(2) Indicator Attention Heatmap
The attention map by category indicates that major indicators differ greatly between fault categories. The main features of normal samples are spectral flatness, while minor outer ring defects show strong dependence on DFA. As the severity of the fault increases, several categories become more prominent with variance and root mean square, indicating a transition from structural/frequency descriptors to amplitude-related statistical features.
The MC-PINN-GCN is currently targeted at rolling bearing vibration fault diagnosis, but the model idea can be generalized to:
• Gearbox fault diagnosis;
• Rotor imbalance, rubbing, and looseness diagnosis;
• Motor mechanical fault and compound fault diagnosis;
• State recognition under multi-conditions, variable speed conditions;
• Less sample, cross-conditions, and domain generalization diagnosis;
• PMH tasks requiring "data evidence + physical mechanism evidence" joint explanation.
Click to download: Complete data, Python code
2. Friends who like this can click to follow, give the article a "watch", share on social media or discuss groups.
Previously excellent content:  
Rapid Paper | Based on 2D-SWinTransformer+1D-CNN-SENet Parallel Fault Diagnosis Model  
Bearing Life Prediction Major Update! Added a collection of CNN-BiGRU-Attention models + rich visualization charts  
Multimodal - Fault Diagnosis | Large kernel convolution opens a new era in vision!  
Superior! Write directly in one zone! Based on SSA+Informer-SENet fault diagnosis model  
Multi-source Information Fusion: Data layer fusion + feature layer fusion fault diagnosis models!

## Images

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
