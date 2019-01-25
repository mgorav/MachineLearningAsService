# ML As A Service Using MNIST Dataset

The business value of data science is all about taking the valuable model to the production. Really!! Actually it's about pipeline and not model. At "Gonnect" we are convinced deployment of the model as part of workflow is suboptimal. In order to make "Data Science" truly "agile", we need to think about deployment of complete ML pipeline. A typical ML pipeline consist of following steps:

- Data transform
- Feature extraction & pre-processing
- ML model
- Prediction transformation

**NOTE:** ETL is an intrinsic part of the pipeline 

At add "fun" - "complexity", there are many framework involved in the pipelines:

- scikit-learn
- Spark ML pipelines
- Tensorflow pipelines
- Keras pipelines
- pytorch pipelines

At "Gonnect", we believe give the power to the "Data Scientist" to choice the framework of there choice. This would be ideal.  Check out the github project, which demonstrates dockerization of ML model and exposing them are REST API (Microservices). As a result, it can be deployed on kubernetes cluster on any cloud provider of your choice. 

## Pre-requiste

- seldon-core
```
   pip install seldon-core
```

- keras
```
   pip install keras
```

- tensorflow

- s2i (on mac)
```
brew install source-to-image
```

- python 3.6

## Play time

- Wrap the model using s2i to expose NNIST prediction as service

```
s2i build . seldonio/seldon-core-s2i-python36:0.4 deepmnist:0.1
```

- Run the docker container wrapped by s2i to expose MNIST as service

```
sdocker run --name "mnist_prediction_service"  --rm -p 5000:5000 deepmnist:0.1
```

- To test

```
seldon-core-tester contract.json 0.0.0.0 5000 -p
```

```
seldon-core-tester contract.json 0.0.0.0 5000 -p
```

**NOTE** This model can now be easily deployed to cluster and scale as per the business requirements.





