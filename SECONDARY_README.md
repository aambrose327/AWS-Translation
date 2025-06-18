Login to your AWS management console and navigate to Amazon Lex from the search bar.
 ![image](https://github.com/user-attachments/assets/d7fa2a37-334c-4c26-bee1-8b8c131a04ac)

Click on ‘Create Bot’.
In the Creation method, go with ‘Create a blank bot'. Give the chatbot a suitable name and description.
![image](https://github.com/user-attachments/assets/fece3679-0663-44b9-80ff-c7f59865b16f)

For the IAM role, choose ‘Create a role with basic Amazon Lex permissions’ which will automatically create a role for you. Choose ‘No’ for the option Children’s Online Privacy Protection Act (COPPA), leave the rest as default and click Next.
![image](https://github.com/user-attachments/assets/ce8dde6b-1a37-4db8-9ad8-39e8a30c1e7d)

You can choose the language you want to communicate with the bot and can also choose between different voice interaction modules. The Intent classification confidence score threshold is like a confidence bar that the system uses to decide if it's sure enough about what the user meant. For now let’s keep it default and click Done.
![image](https://github.com/user-attachments/assets/4cc24140-44af-44c7-ab10-c9689781446a)

Your empty chatbot has been created! You will lead on the Intent page where we will work on the conversational flow of the chatbot.

In the Intent details, fill in an appropriate Intent name and description.
![image](https://github.com/user-attachments/assets/3e414e5d-9fa5-49df-ab61-1f96e5d508d8)

In the sample utterances, add some inputs that can be asked by the user. Amazon Lex will try to understand the user input by aligning the input with the utterances provide
![image](https://github.com/user-attachments/assets/46146e00-f8bd-4485-b9ff-e5173ca16f3e)

Go to the slots option and click on Add Slot. We need to take the language in which the text to be translated as a slot. For that we need to first create the Slot type. Go back and click on Save Intent. Click on back to Intents list and navigate to slot type, add Slot type.
Choose ‘Add blank slot type’ and give a name to the slot type (here ‘language’).
![image](https://github.com/user-attachments/assets/254b8734-f0b2-4cae-ab55-809428155474)

Add some languages as Slot type values similar to given below:
![image](https://github.com/user-attachments/assets/acf04388-b3a5-47ba-801b-8875e7a980fb)

Click on Save slot type. Navigate back to the Intents to use this slot type for our slot.
![image](https://github.com/user-attachments/assets/4a41ec00-1f6e-414a-b723-ffd7f2ee4832)

Click on Add Slot. Give the slot name and choose the slot type ‘language’ previously made. Write the prompt where the chatbot asks for user choice for language translation.
Click on Add.
Create another slot ‘text’ which takes the text to be translated as an input. Choose AMAZON.FreeFormInput as the slot type option and enter a suitable prompt asking for the text to be translated. Click on Add.
![image](https://github.com/user-attachments/assets/28c19c3b-9534-4054-88ea-c817bf47364c)

We can add some more utterances specifying the Slots. For example : Instead of ‘I want to translate’ , if user inputs ‘I want to translate to French’ with the language specified in the starting intent itself, it should not ask for the language again by running the language prompt. Instead we can specify Slots like below:
![image](https://github.com/user-attachments/assets/a6fb584c-8165-4f71-9ebb-d55b531bf45a)

We can also add an Initial response to the initial intent as a feedback message.
![image](https://github.com/user-attachments/assets/2e0d4dd3-b697-4d74-b1dc-1e7568ef117e)

Fulfilment runs the Lambda function to fulfil the intent and informs users about it’s status once it is complete.
Write a suitable prompt on successful fulfilment and in case of a failure.
![image](https://github.com/user-attachments/assets/9745bdb4-751a-47bd-b833-d2304aacf4fd)

Click on ‘Advanced Options’ and check ‘Use a Lambda function for fulfilment’. Click on update options.
We can also provide a Closing message after completion of the intent.
![image](https://github.com/user-attachments/assets/235cd4bf-d0c9-4db8-a199-71613e24f7b9)
Click on ‘Save Intent’.

From your AWS management console, navigate to IAM from your search bar.
Navigate to roles and Create Role. This role will be used for the Lambda function to provide basic Lambda execution permissions and access to Amazon Translate.
Select the trusted entity type as AWS service and select Lambda as the use case. Click on Next.
![image](https://github.com/user-attachments/assets/56641d51-f2ed-4b6b-a9a3-517723c66abb)

Attach the following policies to the role :
TranslateFullAccess
AWSLambdaBasicExecutionRole
Click on Next. Enter a suitable name and description for the role and Create Role.
![image](https://github.com/user-attachments/assets/7b142cc7-ee7a-4239-acc2-f0e9dddd8b31)

This role will be used for the Lambda function permission.

From your AWS management console, search for Lambda from your search bar.
![image](https://github.com/user-attachments/assets/4052efc4-de9a-4742-a525-9e5e14be86ab)

Click on Create Function. Give the function a suitable name and choose the runtime as Python 3.12.
Choose the previously created role by toggling the default execution role option. Keep the rest of the values as default and ‘Create Function’.
Let us first look at the Lambda code

Click on ‘Deploy’ to deploy the Lambda function.

To test the Lambda function, click on Test and configure the Test event.
Give a suitable name to the test event and keep the Event JSON in the format below:
![image](https://github.com/user-attachments/assets/1e7daa52-c042-4aa5-a51b-b00e1be0abd3)

The reason that we are providing this format is because your Lambda function gets an input from the Amazon Lex in this specified format.
Save the test event and click on Test again to Invoke the event.
![image](https://github.com/user-attachments/assets/43e3c03b-aa9a-46fa-9ef9-6e961b55ae12)

Navigate to the Intent page of your previously created Chatbot. Before testing it, we need to specify the Lambda function to be used by Lex.
Click on the settings option present on your top right of the chatbot window and choose the Source of Lambda function as your previous created function.
Now you are ready to go! 
![image](https://github.com/user-attachments/assets/faa054ab-f6f5-469d-be4d-aef5edcc09ec)






