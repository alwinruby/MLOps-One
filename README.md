# MLOps-One


### Deep Learing Library

[Pytorch Lightning](https://lightning.ai/pages/open-source/) (Pytorch lightning is a wrapper around pytorch) will be used, it automates a lot of engineering code and comes with many features.


* How to get the data?

    Using Hugging Face

* How to process the data?


        DataModules are more structured definition, which allows for additional optimizations such as automated distribution of workload between CPU & GPU. Using DataModules is recommended whenever possible!

        A DataModule is defined by an interface:

        prepare_data (optional) which is called only once and on 1 GPU -- typically something like the data download step we have below
        setup, which is called on each GPU separately and accepts stage to define if we are at fit or test step
        train_dataloader, val_dataloader and test_dataloader to load each dataset
        A DataModule encapsulates the five steps involved in data processing in PyTorch:

        Download / tokenize / process.
        Clean and (maybe) save to disk.
        Load inside Dataset.
        Apply transforms (rotate, tokenize, etc…).
        Wrap inside a DataLoader.

        __See data.py__

* How to define dataloaders?

        To make a working model out of a LightningModule, we need to define a new class and add a few methods on top.

        A LightningModule is defined by an interface:

        init define the initialisations here
        forward what should for a given input (keep only the forward pass things here not the loss calculations / weight updates)
        training_step training step (loss calculation, any other metrics calculations.) No need to do weight updates
        validation_step validation step
        test_step (optional)
        configure_optimizers define what optimizer to use

        __See modal.py__

* How to declare the model?

         __See modal.py__

* How to train the model?

        The DataLoader and the LightningModule are brought together by a Trainer, which orchestrates data loading, gradient calculation, optimizer logic, and logging.

        Setup Trainer and can customize several options, such as logging, gradient accumulation, half precision training, distributed computing, etc.

        Logging of the model training

        __See train.py__


        It will create a directory called logs/cola if not present. You can visualise the tensorboard logs using the following command

        tensorboard --logdir logs/cola

        Callback is a self-contained program that can be reused across projects.


* How to do the inference?

        Once the model is trained, we can use the trained model to get predictions on the run time data. Typically Inference contains:

        Load the trained model
        Get the run time (inference) input
        Convert the input in the required format
        Get the predictions

        __See interface.py__





