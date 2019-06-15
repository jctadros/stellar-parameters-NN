# stellar-parameters-NN

Development in astronomical observation technology and the emergence of large-sky surveys (GAIA- RVS, LSST, APOGEE) in the last decade will result in the reveal of huge stellar spectral data. Therefore, automated processing techniques are needed for stellar parametrization and sta- tistical exploration of spectrum-parameter dependencies. We devise a deep neural net- work model with the capability of inverting four stellar parameters (Teff,log(g),[Fe/H],vsin(i)) for A and FGK stars, when trained on synthetic spectra. The synthetic spectra were based on models generated by ATLAS9 and by the spectrum synthesis code SYNSPEC48. In this approach, the existence of a functional relation mapping the spectral fluxes to the four stellar parameters is assumed, accordingly, the primary task of the network is to learn this relation. 

* 0.join.py : joins the different databases and stack them in one indexed database
* 1.label_study.py : explores the created datasets just so to see the distribution of the labels in the label space. To check the spread, mean, distribution etc of the data.
* 2.pre_processing.py : This code standarizes the label datasets using the individual means and standard
deviations corresponding to each label. And shuffle the entire datasets and then
stores them in a new h5py database file containing the shuffled spectra, and
standarized labels together with the individual mean and standard deviations.
The mean and standard deviations are stored so that re-standarization can be performed
in the testing phase (file 4.test.py)
* 3.train.py : creates a network composed of two 1-dimensional convolutional layers, 1-dimensional maxpooling layers, and two dense layers linearily stacked in Sequential mode. The model is optimized by the first-order adaptive gradient-based optimization scheme ADAM equipped with EarlyStopping and ReduceLRonPlateau callbacks.
* 4.test.py : After training is done and the model's wieghts are saved, the network can be thus used to predict on new datasets. This code
applies the converged model to new data. The testing dataset is noised using gaussian noise prior to test.
* jacobian.py : explores the input-output layers dependencies by calculating the jacobian of the network

