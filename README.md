# CodeNebula
Automating documentation to enhance accuracy and accessibility for developers. Utilizing Python method functions and predefined docstrings to extract key details. Fine-tuned CodeT5 and CodeBert models provide concise and high-quality summaries for project understanding and development.
Below are the steps involved:
1. Selecting the appropriate dataset: BOA Dataset is chosen as it is benchmarked and has passed numerous quality tets. It also consists of 1558 matured github repositories that contain numerous python function with docstrings.Here is a snapshot of what this dataset looks like:
   ![image](https://github.com/LaurynArora1/CodeNebula/assets/79740749/8554df9c-8d27-4a4a-a18e-1ffd49b5b151)

3. Pre-processing the data:
   1. Loop through all the repositories and look for python files and then convert these python function code to an AST tree and traverse the AST to obtain the function name and function code.![image](https://github.com/LaurynArora1/CodeNebula/assets/79740749/f4971982-a87c-48e4-ab39-50ce274851ee)
   2. Within the function's code resides its docstring, which provides informative comments about the function's purpose and behavior. This docstring typically contains various attributes, but we're particularly interested in the short description and long description attributes. By combining these attributes, we can construct a summary of the function.
![image](https://github.com/LaurynArora1/CodeNebula/assets/79740749/777d22a8-719d-46b5-a272-5abd20c3df91)

2. To check the the BLEU score for our pre-processed dataset using the pre-trained CodeT5 model:
   1. Tokenize each code snippet using a pretrained RobertaTokenizer and generate a summary using a fine-tuned CodeT5 model.
   2. Calculate the BLEU score between the generated summary and the existing summary for each code snippet.
   3. Save the results, including the code snippet, existing summary, generated summary, and BLEU score, into a DataFrame.
![image](https://github.com/LaurynArora1/CodeNebula/assets/79740749/0e63ac4b-1b8e-465a-8625-1cd8e6f72527)


4. To fine-tune the model on the pre-processed dataset:
   1. Load dataset and split into training/validation sets. Utilize CodeT5 model for summarization.
   2. Define training arguments, including batch size, epochs, and evaluation strategy.
   3. Implement EarlyStoppingCallback and compute_metrics function for BLEU score calculation.
   4. Train the model, save the fine-tuned model, and tokenizer for future use.
 
![image](https://github.com/LaurynArora1/CodeNebula/assets/79740749/9587afe7-149e-4985-80d4-2f27efadf43a)
References:
1. https://boa.cs.iastate.edu/stats/index.php
2. https://huggingface.co/Salesforce/codet5-base-multi-sum

