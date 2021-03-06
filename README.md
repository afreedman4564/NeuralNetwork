# Alphabet Soup Funding Success

## Objective: determine, using Neural Network, whether applicants for funding will be successful

### Preprocessing of data
- Variable used as target/independent variable: IS_SUCCESSFUL
- Preliminary features leveraged:
    - CLASSIFICATION
    - USE_CASE
    - ORGANIZATION
    - STATUS
    - INCOME_AMT
    - SPECIAL_CONSIDERATIONS
    - ASK_AMT
    
- Variables included in original dataset and subsequently removed:
    - EIN
    - NAME

*Rationale for removal: id of business name and id not believed impactful on success

### Data Compilition
- Data preprocessing
    - Application Type streamline
        - Consolidate Application Types with with frequency less than 500
        - Application Type distribution prior to consolidation
![](/Images/ApplicationTypeOriginal.png)

        - Application Type distribution post consolidation
![](/Images/ApplicationTypePreprocessing.png)


    - Classification steamline
        - Consolidate Classification valuest with less than 1,000 frequency
        - Classification distribution prior to consolidation
![](/Images/ClassificationOriginal.png)


        - Classification distribution post consolidation
![](/Images/ClassificationPreprocessing.png)


    - Leverage get_dummies function to convert categorical text values to numbers
    - Illustrative snipit of get_dummies output
![](/Images/get_dummies_output.png)


    - Use StandardScaler function to scale feature data post Application Type and Classification consolidation, along with get_dummies transformation
![](/Images/XTrainedScaled.png)


### Model Training
    - Apply two hidden layers
    - First hidden layer to include 50 neurons utilizing relu activation function
    - Second hidden layer to include 75 neurons utlizing relu activation function as well
    - Relu was used due to:
        - Expedited cycle time to learn
        - Leverages less complex computational approach relative to other activation functions
        - Given above rationale, preliminary approach was a simple approach that could be refined further to achieve strong, more accurate results
    - Sigmoid activation function also leveraged due to:
        - Values lie between 0 and 1
        - Given objective is to predict success, probability as output is fitting

### Model Evaluation
    - Model target of 75% accuracy was not achieved in the original run
![](/Images/PreliminaryModelAccuracy.png)


    - Improvements made to improve model performance:
        - Features utilized:
            - Dropped EIN, STATUS, and SPECIAL_CONSIDERATIONS
                -STATUS and SPECIAL_CONSIDERATIONS distributions values were unilateral, impacting success little
                    - STATUS distribution
![](/Images/StatusDistribution.png)

                    - SPECIAL_CONSIDERATIONS distribution
![](/Images/SpecialConsiderationsDistribution.png)

            - Consolidated NAME and INCOME_AMT to better distribute values to make easier for machine to learn
                - NAME
                    - Original distribution
![](/Images/NameOriginalDistribution.png)

                    - Post consolidation distribution
![](/Images/NamePostConsolidationDistribution.png)


                - INCOME_AMT
                    - Original distribution
![](/Images/IncomeAmtOriginalDistribution.png)

                    - Post consolidation distribution
![](/Images/IncomeAmtPostConsolidationDistribution.png)



        - Three additional hidden layers added and tanh activation function
            - First three hidden layers utilizes relu activation function and 75, 50 and 25 neurons respectively
            - Fourth hidden layer has 10 neurons and utilizes sigmoid activation function
            - Fifth hidden layer has 5 neurons and utlizes tanh activation function due to:
            - Reason for introducing tanh is appropriate for classification between two classes
            - Epochs reduced from 200 to 25 to avoid overfitting

        - Optimized accuracy improved and exceeds 75%, the target threshold
![](./Images/OptimizeAccuracy.png)

    

 ### Summary
    - Objective was achieved, as target met
    - Steps taken to engineer data to yield more desirable outcome
    - Additional activation functions introduced that will support classification objective   
    - Recommendations for future enhancements:
        - Continue to test additional data preprocessing approaches
        - Evaluate how more/fewer neurons at hidden layer level
        - Assess impact of activation functions at various stages of neural network
        - Deploy a function to optimize epochs run
        - Evaluate Supervised and Unsupervised techniques to determine how additional machine learning techniques bare out