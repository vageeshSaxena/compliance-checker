# complianceChecker: Checking Compliances for Responsible Guidelines in Authorship Attribution Approaches in NLP

**Abstract:** Authorship Attribution (AA) approaches in Natural Language Processing (NLP) are important in various domains. However, they pose ethical, legal, and societal (ELS) challenges that remain under-explored within the legal and NLP community. Our research presents a comprehensive framework of responsible guidelines for researchers and stakeholders (designers, developers, testers, and end-users), encompassing the three phases of the AA life cycle: design, development, and deployment. The framework comprises four key principles: privacy and data protection, transparency and fairness, discrimination and unintended biases, and societal impact. It allows stakeholders to identify potential issues and to weigh the benefits of AA research against privacy, transparency, discrimination, and bias in AA applications, thereby mitigating potential risks and harm for the greater good of society. These guidelines enable researchers and practitioners to justify their decisions and assist ethical committees in promoting responsible practices and identifying ethical concerns related to NLP-based AA approaches, ultimately ensuring the responsible development and deployment of AA tools for the benefit of society.

**complianceChecker:** ComplianceChecker is a tool that utilizes chatGPT and LangChain for conducting Q&A analyses on documents from the Authorship Attribution literature. Its primary function is to cross-check whether these documents comply with the responsible guidelines we have established in our research. The tool is designed to automatically evaluate adherence to our guidelines across a selected sample of studies (67 in our case) in the field of Authorship Attribution. The aim is to systematically assess and verify how these studies conform to the suggested responsible practices.

# Setup
This repository is tested on Python 3.10 and [conda](https://docs.conda.io/projects/miniconda/en/latest/). First, you should install a virtual environment:
```
conda create -n RAA python=3.10
```

To activate the conda environment, run:
```
conda activate RAA
```

Then, you can install all dependencies:
```
pip install -r requirements.txt
```

# Methodology
**Literature Collection:** To collect the literature, we use the [RESP](https://github.com/monk1337/resp) project to download research papers from the first 4 pages of Arxiv. Please note that all the collected pdfs must be places under a folder called "pdfs" in the root directory. For reproducibility purposes, we suggest using the following keywords:

``` keywords = ['Authorship Attribution', 'Authorship Attribution Darknet', 'Authorship Attribution Dark Web', 'Authorship Attribution Cybercrime', 'Authorship Attribution Human Trafficking', 'Authorship Attribution Forensic Analysis'] ```

In our analysis, we collected 67 literature studies from the abovementioned list of keywords. 

**Generating Queries:** To generate the queries, we took the guidelines from our research and appended "If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. " to each guideline under each category.

``` queries = {
    "privacy" :  [
    "Does the Authorship Atttribution research/application involve a high level of risk, necessitating a Data Protection Impact Assessment (DPIA)? High-risk scenarios may include biometric identification, law enforcement, or justice system usage. If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Does the Authorship Atttribution processing encompass extensive automated processing leading to decisions with legal or significant effects on individuals? Are measures in place to prevent identity disclosure, reputational damage, or legal consequences? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Is there a scientific purpose or objective justifying exemptions from GDPR provisions? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Is data processing confined to the original purpose for which it was collected? Is there periodic assessment and review to ensure ongoing relevance? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Does the dataset contain information enabling the identification of individuals? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Have adequate safeguards like anonymization, encryption, data minimization, and security procedures been implemented to minimize risks and protect individual rights? Are these measures in line with guidelines from research and academic organizations, with ethical oversight? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Is the information provided to individuals about data processing clear, complete, and correct? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
],
    
    "bias" : [
    "Is there a specific label or target for each data instance, and how were these labels obtained? For manually annotated data, please provide details about the number of annotators, their backgrounds, and any measures taken to mitigate label bias. If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Does the training dataset sufficiently represent the entire authorship landscape, and what steps were taken to mitigate selection bias? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Are there correlations between authors in the dataset and specific demographic attributes or population characteristics? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Does the dataset cover multiple text genres or domains, and if not, what actions were taken to prevent biases related to domain and genre? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Is there a class imbalance in the dataset, and what measures were implemented to avoid over-representing certain authors? Describe any sampling strategies used to address potential sampling bias. If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "What feature extraction techniques were employed during training, and was fine-tuning performed on the target data? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "What precautions were taken to prevent overfitting and underfitting during model training? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Do the chosen evaluation metrics align with the primary task objectives, and what insights can be provided about model generalization and robustness? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Were independent blind assessments conducted by external evaluators, and can information about their backgrounds and diversity be provided? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. "
],
    
    "transparency" : ["Are any experiments conducted to gain insights into the model’s decision-making processes? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no.",
                     "Are any error-analysis experiments conducted to understand false-positive and true-positive predictions? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no.",
                     "Are any explainability/Interpretability experiments conducted to understand model learning and model predictions? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no." ],
    
    "risk" : [
    "Is there a disclaimer to alert readers to potentially harmful content in the research? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Does the Authorship Atttribution processing encompass systematic and extensive automated processing that leads to decisions with legal or significant effects on individuals? Are measures in place to prevent identity disclosure, reputational damage, or legal ramifications? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Does the scope of the Authorship Atttribution model align with its intended purpose to minimize potential misuse? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Is there a mechanism to mitigate the risk of potential misuse and abuse, including scenarios involving targeted harassment, social engineering, or the creation of deceptive content falsely attributed to others? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Are there mechanisms for human oversight and intervention to review and reject content with ethical concerns? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "What measures are in place to minimize the potential trauma experienced by individuals during the design, development, and deployment stages? Are there regular check-ins among team members to ensure clear communication and provide essential support for maintaining a healthy and safe working environment? Is mental health and psychological support offered to team members dealing with harmful text? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Is there a routine schedule of audits and updates to the Authorship Atttribution model to anticipate and address potential ethical challenges? Do these audits and updates help ensure the model remains aligned with evolving ethical standards and societal expectations? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. ",
    "Are efficient algorithms and training strategies given priority to minimize the carbon footprint and energy consumption? Is carbon tracking employed to monitor and quantify carbon emissions during Authorship Atttribution model training, aiding in optimization and offsetting strategies? If the relevant details are not available, just say Info not available. Otherwise answer it as yes or no. "
]
}
```

# Analysis

To generate the analysis, please run the generateStats.ipynb file. For better understanding of the code, click [here](https://www.youtube.com/watch?v=oZFAxHjlB-4).
