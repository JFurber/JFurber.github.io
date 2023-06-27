&nbsp;

<h1 style="text-align: center;"> Isaac Newton Institute: Summer School on Mathematics of Movement  </h1>

<h2 style="text-align: center;"> Abstract </h2>

The purpose of the current study is to establish a modelling framework to understand the movement of European badgers (Meles meles) within their environment. It is widely understood that badgers play a crucial role in the transmission of bovine tuberculosis (bTB), where bTB is a serious disease of cattle and has a significant economic impact on farmers. However, despite all the GPS data, ecologists still do not understand what they can learn from the data about fine-scale badger movement. A key research question we would like to answer is can we generate a dynamical model to explore badger movement?

To model the movements, we are generating a stochastic Brownian motion model using badger GPS tracking data. Such an approach has been successful in describing the movements of free-ranging elk and their avoidance of vehicles and humans but has yet to be applied to the study of badgers. 

The model is created using data driven methods, where it is parametrized using GPS data. The modelling framework will allow us to answer key ecological questions: How does badger movement affect the spread of bTB? How does the weather affect badger movement? With the role badgers play in the spread of bTB, the answer to these questions could be crucial in the role of strategy planning.

We present results on the parameterized model with the data. This includes the generation of an energy potential and the estimation of a noise term. We have also analysed the differences between male and female badgers to understand different transitions. By simulating these differences, we have created a dynamical model that explores badger movement, and we can now start answering the key ecological questions.


---

<h2 style="text-align: center;"> Generated Trajectory </h2>

Below is the animation linked to Figure 3, where the 'badger' can be seen to be moving along its trajectory. The initial position links to an individual badger that is being monitored at the park, and the diffusion term of the badger has been calculated. 

The animation is plotted every two iterations to show a smoother movement of the badger following its trajectory, in comparison to every thirty-five iterations in Figure 3. Also, only the first 10,000 iterations have been animated out of the 100,000 generated. But, this is a great tool to have a better visual of the badger movements in the park.

<p align="center">
<img src="14M_10000.gif">
</p>

---
<h2 style="text-align: center;"> Extended Dynamic Mode Decomposition </h2>

<p> This section compliments the box on Extended Dynamic Mode Decomposition (EDMD). For information on EDMD and algorithm, see references [5] and [7]. In essence,the eigenvalues and eigenfunctions of the Koopman Operator capture the long-term dynamics of the observables (for example the coordinates) of the dynamical system. EDMD is used to compute an approximation for the Koopman Operator directly. Then, we analyze the Koopman operator via its spectrum. </p>

<p> One requirement for using EDMD is uniformly spaced time intervals. Due to the nature of the GPS collection, unfortunately, we do not have uniform time intervals. We overcome this by interpolating the data. Here, we assume that the badgers are moving in a linear fashion between coordinates, and they are moving the same speed. We need to find a lag time so the space is not too small that we lose the dynamics, and not too large that we are unable to see the dynamics. For example, if we interpolate so we have 2-minute intervals, then we are literally assuming the badgers are moving in a straight line between points A and B. Yet, by reference [6] it is proved by <i> dead reckoning </i> that badgers do not take a linear route. If we use 35-minute intervals, then we are unable to see anything in the results. Hence, we interpolate the data for every 17.5 minutes. Whilst this is assuming we know the position halfway, it gives more ‘freedom’ for the badger between each point. </p>

<p> The results using the 17.5 minute interpolated data are presented. The eigenvalues can be seen in Figure 4, and the first eight eigenfunctions that correspond to the first eight eigenvalues are seen below. The eigenfunctions depict where there are energy barriers within the park (i.e. where there are few transitions between areas). </p>

<figure>
<p align="center">
<img src="Woodchester_EDMD_K_Eigenfunctions.png">
</p>
      <figcaption> <em>Figure</em>. The first eight eigenfunctions corresponding to the first eight eigenvalues seen in Figure 4. The first eigenfunction (Eigenfunction 0) is constant, as expected. The second eigenfunction (Eigenfunction 1) highlights there are very few transitions between the bottom and the top of the park. The following eigefunctions highlight where the next energy barriers are within the park. </figcaption>
</figure>

&emsp;

<p> When we compare the clustered eigenfunctions against the initial K-Means clustering of the data we see that the clustering are very similar. (Using optimisation tools, it was shown that eight is the optimal amount of clusters for the data set). One benefit of using EDMD over similar K-Means clustering of the data, is that EDMD is looking at the dynamics of the system. Whereas K-Means clustering is looking at the Euclidean distance of points to a centroid mean. From this perspective, EDMD is a better representation of the clusters. Yet, the disadvantage is that the data does need to be interpolated to use the method. Nevertheless, through the use of EDMD we are able to see the natual clusters of the park and where the main territories of the badgers lie. </p>

<figure>
<p align="center">
<img src = "17_5_Cluster8_2.png" 
      width="350"  />
<img src = "Cluster8_2.png" 
      width="350"  />
      <figcaption> <em>Figure</em>. <b>Left</b>: The eight Koopman eigenfunctions clustered using K-Means. <b>Right</b>: The original GPS data clustered using K-Means clustering. </figcaption>
</p>
</figure>


___
<h2 style="text-align: center;"> Transition Probabilities </h2>

<p> Using the clusters generated with EDMD, we allocate each coordinate (from the 17.5 minute interpolated data) a cluster. Then, we are able to calculate the transition at each time point. There are eight clusters in total, and we add a ninth state. This state is when the badgers no longer have GPS data, so in essence is a ‘removed’ state from the data. There is no returning to the park once they are in this state, which is why in Figure 5 there are no return arrows to any of the states. The transition matrix corresponding to Figure 5 is seen below. State 1 starts on the far left and moves up and around the park clockwise, until it reaches the crossing to go to the bottom of the park. As is can be seen, there are very strong probabilities of staying in the original cluster at the next time point, with few transitions to the cluster ‘next door’. There are no jumps across the park in a single time step. This was to be expected as the clusters are made up of multiple territories. Hence, showing that the badgers stay generally amongst multiple territories in their cluster, rather than wandering to others. This could have implications if wanting to control the spread of bovine Tuberculosis. </p>

$$ \begin{pmatrix}
0.970600858 & 0.008583691 & 0 & 0 & 0 & 0 & 0.019527897 & 0 & 0.001287554 \\
0.002541296 & 0.988193562 & 0.00259424 & 0 & 0 & 0 & 0.005664972 & 0 & 0.00100593 \\
0 & 0.008511409 & 0.96957624 & 0.015030786 & 0 & 0.002897501 & 0.002716407 & 0 & 0.001267657 \\
0 & 0 & 0.004845688 & 0.989789443 & 0.003749639 & 0.000519181 & 0 & 0 & 0.001096048 \\
0 & 0 & 0 & 0.003072474 & 0.987167902 & 0.009036689 & 0 & 0 & 0.000722935 \\
0 & 0 & 0.001585571 & 0.000594589 & 0.020017838 & 0.970468735 & 0.006044991 & 0 & 0.001288277 \\
0.013837946 & 0.01933978 & 0.002667556 & 0 & 0 & 0.010003334 & 0.952484161 & 0.000166722 & 0.0015005 \\
0 & 0 & 0 & 0 & 0 & 0 & 0.000695894 & 0.997912317 & 0.001391788 \\
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 
\end{pmatrix}  $$
___

<h2 style="text-align: center;"> Bibliography </h2>

[1] Brillinger, D., Preisler, H., Ager, A., Kie, J., and Service, U. *The use of potential functions in modelling animal movement*. Data Analysis from Statistical Foundations: A Festschrift in Honour of the 75th Birthday of DAS Fraser (05 2001).

[2] Burt, W. H. *Territoriality and home range concepts as applied to mammals*. Journal of Mammalogy 24, 3 (1943),
346–352.

[3] Do Linh San, E., Ferrari, N., and Weber, J.M. *Spatio-temporal ecology and density of badgers meles meles in the swiss jura mountains*. European Journal of Wildlife Research 53 (2007), no. 4, 265–275.

[4] Downs, J., Horner, M., Lamb, D., Loraamm, R. W., Anderson, J., and Wood, B. *Testing time-geographic density estimation for home range analysis using an agent-based model of animal movement*. International Journal of Geographical Information Science 32, 7 (2018), 1505–1522.

[5] Klus, S., Koltai, P., and Schutte, C. *On the numerical approximation of the Perron-Frobenius and Koopman operator*. Journal of Computational Dynamics (2015).

[6] Magowan, E.A., Maguire, I.E., Smith, S., Redpath, S., Marks, N.J., Wilson, R.P., Menzies, F., O’Hagan, M., and Scantlebury, D.M., *Dead-reckoning elucidates fine-scale habitat use by European badgers Meles meles*. Animal Biotelemetry 10 (2022), no. 1, 10.

[7] Niemann, J.H., Klus, S., and Schutte, C., *Data-driven model reduction of agent-based systems using the Koopman generator*. PLOS ONE 16 (2021), no. 5, 1–23.

[8] Preisler, H., Ager, A., Johnson, B., and Kie, J. *Modeling animal movements using stochastic differential equations*. Environmetrics 15636 (11 2004), 643–657.

[9] Preisler, H. K., Ager, A. A., and Wisdom, M. J. *Analyzing animal movement patterns using potential functions*.
Ecosphere 4, 3 (2013), 1–13.


