
# RAG Application CDK Python project!

![rag_with_opensearch_arch](./rag_with_opensearch_arch.svg)

This is an QA application with LLMs and RAG project for CDK development with Python.

The `cdk.json` file tells the CDK Toolkit how to execute your app.

This project is set up like a standard Python project.  The initialization
process also creates a virtualenv within this project, stored under the `.venv`
directory.  To create the virtualenv it assumes that there is a `python3`
(or `python` for Windows) executable in your path with access to the `venv`
package. If for any reason the automatic creation of the virtualenv fails,
you can create the virtualenv manually.

To manually create a virtualenv on MacOS and Linux:

```
$ python3 -m venv .venv
```

After the init process completes and the virtualenv is created, you can use the following
step to activate your virtualenv.

```
$ source .venv/bin/activate
```

If you are a Windows platform, you would activate the virtualenv like this:

```
% .venv\Scripts\activate.bat
```

Once the virtualenv is activated, you can install the required dependencies.

```
(.env) $ pip install -r requirements.txt
```

To add additional dependencies, for example other CDK libraries, just add
them to your `setup.py` file and rerun the `pip install -r requirements.txt`
command.

Before synthesizing the CloudFormation, you should set approperly the cdk context configuration file, `cdk.context.json`.

For example:

```
{
  "opensearch_domain_name": "open-search-domain-name"
}
```

Now this point you can now synthesize the CloudFormation template for this code.

```
(.env) $ export CDK_DEFAULT_ACCOUNT=$(aws sts get-caller-identity --query Account --output text)
(.env) $ export CDK_DEFAULT_REGION=us-east-1 # your-aws-account-region
(.env) $ cdk synth --all
```

Now we will be able to deploy all the CDK stacks at once like this:

```
(.env) $ cdk deploy --require-approval never --all
```

Or, we can provision each CDK stack one at a time like this:

#### Step 1: List all CDK Stacks

```
(.env) $ cdk list
RAGVpcStack
RAGOpenSearchStack
RAGSageMakerStudioStack
EmbeddingEndpointStack
LLMEndpointStack
```

#### Step 2: Create OpenSearch cluster

```
(.env) $ cdk deploy --require-approval never RAGVpcStack RAGOpenSearchStack
```

#### Step 3: Create SageMaker Studio

```
(.env) $ cdk deploy --require-approval never RAGSageMakerStudioStack
```

#### Step 4: Deploy LLM Embedding Endpoint

```
(.env) $ cdk deploy --require-approval never EmbeddingEndpointStack
```

#### Step 5: Deploy Text Generation LLM Endpoint

```
(.env) $ cdk deploy --require-approval never LLMEndpointStack
```

**Once all CDK stacks have been successfully created, proceed with the remaining steps of the [overall workflow](../README.md#overall-workflow).**


## Clean Up

Delete the CloudFormation stacks by running the below command.

```
(.env) $ cdk destroy --all
```

## Useful commands

 * `cdk ls`          list all stacks in the app
 * `cdk synth`       emits the synthesized CloudFormation template
 * `cdk deploy`      deploy this stack to your default AWS account/region
 * `cdk diff`        compare deployed stack with current state
 * `cdk docs`        open CDK documentation

Enjoy!

## References

 * [Build a powerful question answering bot with Amazon SageMaker, Amazon OpenSearch Service, Streamlit, and LangChain](https://aws.amazon.com/blogs/machine-learning/build-a-powerful-question-answering-bot-with-amazon-sagemaker-amazon-opensearch-service-streamlit-and-langchain/)
 * [AWS Deep Learning Containers Images](https://docs.aws.amazon.com/deep-learning-containers/latest/devguide/deep-learning-containers-images.html)
 * [OpenSearch Popular APIs](https://opensearch.org/docs/latest/opensearch/popular-api/)
