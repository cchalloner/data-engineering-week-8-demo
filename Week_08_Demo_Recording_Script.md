# Week 8 Demo Recording Script

Read the narration while showing the matching notebook step. Instructions in brackets are not spoken. Run the notebook before recording, using the course environment and demo folder.

## Step 1: Import the tools

[Show and run the code cell under this heading.]

We will reuse the tools for missing values, category encoding, and scaling. We also need tools to split the rows, train the model, and check prediction error. The first output shows the scikit-learn version in this Python environment. We are using version one point nine. The model choice is LinearRegression. Our work is to prepare the inputs, train it correctly, and explain its predictions.

## Step 2: Inspect the data

[Show and run the code cell under this heading.]

Each row describes one completed service request. Look at the first rows and the missing-value counts. We want to predict actual work minutes. That column is the target. Features are the input columns we use to make the estimate. They must contain information we know when the request arrives. Resolution steps are recorded after the work finishes, so they cannot help us make an earlier estimate without giving the model information it would not have at that time.

## Step 3: Define the target and features

[Show and run the code cell under this heading.]

Put the input columns in X and actual work times in y. We remove the three rows with missing actual times. We need known outcomes to train the model and check its predictions. We keep missing input values because the pipeline will fill them. Leave out request ID and resolution steps. The ID has no chosen role in predicting work time, and the steps are known too late. The assertions check our choices. We now have one hundred seventy-seven rows.

## Step 4: Split before fitting

[Show and run the code cell under this heading.]

We split before the preparation steps learn from the data. There are one hundred thirty-two training rows and forty-five test rows. The training rows teach the preparation steps and model. We save the test rows to check predictions afterward. Random state eight gives us the same split on repeated runs. This random split fits our separate practice requests, but it does not prove these test rows cover every future request type.

## Step 5: Build the data-preparation steps and model

[Show and run the code cell under this heading.]

The numerical features first receive missing-value replacements, then scaling. The categorical features receive replacements, then one-hot encoding. ColumnTransformer applies the correct steps to each group. Pipeline connects those steps to LinearRegression. At this point, we have defined the steps but have not trained them. We keep scaling to practice earlier skills. The target stays in minutes. Full one-hot encoding repeats some information across columns. The model can still predict, but different combinations of coefficients can give the same predictions. If we later study category coefficients, drop equals first can leave a category out for comparison. Keep the current encoder for this demo.

## Step 6: Train the model and make test predictions

[Show and run the code cell under this heading.]

Fit learns the missing-value replacements, scaling values, categories, and regression model from the training data. Predict uses that same preparation to estimate times for the test rows. Look at the results table. Each prediction is next to the correct actual time. The absolute error is the size of the difference, whether the prediction is too high or too low. The predictions remain in minutes because we did not scale the target.

## Step 7: Measure error and compare with a simple guess

[Show and run the code cell under this heading.]

MAE is the average size of the prediction errors, in minutes. Our model has test MAE of about eight point four zero minutes. The baseline always guesses the median training work time and has MAE of about twenty-seven point zero one minutes. Both use the same test requests. The model meets the twelve-minute limit and beats the baseline, so both practice goals pass. We also display R squared, about zero point eight six two. It compares squared errors with always guessing the average actual test time. One means perfect, zero matches that average-value guess, and negative is worse. It has no units and is not percent correct. Our goals still use MAE. We use the original scores for comparisons and round only for display.

## Step 8: Check the workflow

[Show and run the code cell under this heading.]

These checks look for common mistakes. Training and test rows must be different, and each input must match the correct target. Prepared inputs should have the expected rows, matching feature columns, and no missing values or infinity. We need one prediction for every test row. We also check that the medians stored by the imputer match the training medians and that the table’s average error agrees with the MAE function. Transform reuses the preparation already learned from training. We do not fit again on the test data.

## Step 9: Predict work time for new requests

[Show and run the code cell under this heading.]

These new requests do not have actual work times yet. We can estimate their times using the existing pipeline, but we cannot check their errors until the work is done. The second request is missing device count. The pipeline fills it using the training median. Predict uses what the pipeline has already learned. We do not train the model again on these new requests.

## Step 10: Explain the results and their limits

[Show and run the code cell under this heading.]

The plot compares actual and predicted test work times. A point on the dashed line is an exact prediction. Points farther away have larger errors. MAE describes the average, so an individual request can have a bigger error. Passing the practice goals does not prove the model is ready for a real team. The data was created for practice and we used one split. Write down one sentence explaining the MAE and one explaining a limit of the result. For real planning, the team would need testing with real requests that reflect its work. Treat each prediction as an estimate, rather than a promise.

## Recording references

Source links appear at the end of the demo notebook.
