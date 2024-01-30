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
**Literature Collection:** To collect the literature, we use the [RESP](https://github.com/monk1337/resp) project to download research papers from the first 4 pages of Arxiv. For reproducibility purposes, we suggest using the following keywords:

``` keywords = ['Authorship Attribution', 'Authorship Attribution Darknet', 'Authorship Attribution Dark Web', 'Authorship Attribution Cybercrime', 'Authorship Attribution Human Trafficking', 'Authorship Attribution Forensic Analysis'] ```

Please note that all the collected pdfs must be places under a folder called pdf in the root directory.

# Analysis

To generate the analysis, please run the generateStats.ipynb file. For better understanding of the code, click [here](https://www.youtube.com/watch?v=oZFAxHjlB-4).
