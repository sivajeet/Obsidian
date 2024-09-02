*The functionality has to always remain the same, irrespective of what tasks we pick to do?*

- Moving to a new programming language ( Code Translation )
- Moving to a new version ( Can be done along with code translation? )
- Make the code more testable 
- ~~Make the code more container friendly~~ ( Not Interested )
- API Migration
- Style standardization
- Dependency management


# Moving to another programming language (Code Translation)

* Considering Java, Python, C, C++, etc are the programming languages primarily used currently.

## Ideas
#### Using New programming language to help write legacy programming language or moving away
##### Motivation: 
- It will help in maintenance of legacy software, since developers these days are not motivated enough to learn old programming languages like COBOL, MATLAB, etc.
- Even 10 years ago, debates persisted about teaching COBOL in computer science programs[1], there's a growing need for COBOL developers as the current workforce retires [2].
- COBOL is widely used in banking sector, MATLAB is heavily used in Automotive, Medical, primarily for simulation, etc.

##### Current State of Research:
-  Translation of Low-Resource COBOL to Logically Correct and Readable Java leveraging High-Resource Java Refinement, https://llm4code.github.io/assets/pdf/papers/51.pdf
-  Cobol2Vec: Learning Representations of Cobol code, https://www.researchgate.net/publication/358143904_Cobol2Vec_Learning_Representations_of_Cobol_code
-  COBOL programmers are getting harder to find. IBM’s code-writing AI can help, https://research.ibm.com/blog/cobol-java-ibm-z
-  Evaluating LLMs on COBOL, https://bloop.ai/blog/evaluating-llms-on-cobol

##### Resources Available:
- Model trained:  https://huggingface.co/bloopai/mAInframer-34b
- COBOLEval: https://github.com/zorse-project/COBOLEval
- X-COBOL: A Dataset of COBOL Repositories, https://arxiv.org/abs/2306.04892
- Matlab dataset: https://www.mathworks.com/help/matlab/import_export/matlab-example-data-sets.html

#### Moving towards modern/different programming languages
##### Motivation
- LLM's effectiveness on translating real-world code remains largely unstudied.
- New programming languages like Rust. Rust is an emerging programming language designed for both performance and security, and thus many research efforts have been conducted recently to migrate legacy code bases in C/C++ to Rust to exploit Rust’s safety benefits. [3]
- Developers don't have to learn multiple programming languages?

##### Current state of research
- RUSTY: Effective C to Rust Conversion via Unstructured Control Specialization, https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10076938
- Understanding the Effectiveness of Large Language Models in Code Translation, https://www.semanticscholar.org/paper/Understanding-the-Effectiveness-of-Large-Language-Pan-Ibrahimzada/494e2b04fbc78b4bb54f5c9baf7748a83e698b1d
- CodeTransOcean: A Comprehensive Multilingual Benchmark for Code Translation, https://www.semanticscholar.org/paper/CodeTransOcean%3A-A-Comprehensive-Multilingual-for-Yan-Tian/6346dd1e2426e51d2ab8b7eef017714d2d60ed22
- Evaluating Human-AI Partnership for LLM-based Code Migration, https://dl.acm.org/doi/10.1145/3613905.3650896
- Lost in Translation: A Study of Bugs Introduced by Large Language Models while Translating Code, (Zotero)
- Towards Translating Real-World Code with LLMs: A Study of Translating to Rust, https://www.semanticscholar.org/paper/Towards-Translating-Real-World-Code-with-LLMs%3A-A-of-Eniser-Zhang/255ca444da23f51651ff9e259e1d097ecd76b021
- Multilingual Code Co-evolution using Large Language Models, https://www.semanticscholar.org/paper/Multilingual-Code-Co-evolution-using-Large-Language-Zhang-Nie/aef0e3460a0f5c6840891131aeb2036b9f771da5

##### Resources Available:
- https://github.com/rust-lang/rust-repos
- Github on BigQuery: https://cloud.google.com/blog/topics/public-datasets/github-on-bigquery-analyze-all-the-open-source-code, https://console.cloud.google.com/marketplace/details/github/github-repos?pli=1&project=seraphic-being-386515
- CodeNet, Avatar, EvalPlus


#### Challenges
- How to evaluate them? Unit tests, Fuzzying
- Resources(Infastrucutre)




# API Translation
## Motivation
- API migration is an essential step for code migration between libraries or programming languages, and it is a challenging task as it requires detailed comprehension of both source and target APIs. [4]
- The existing work either recommends mapped API names only and requires developers to select specific parameters and return value, or uses encoder-decoder models to directly “translate” the source API code into the target API code without considering the characteristics of APIs. [4]

## Current state of research:
- Hybrid API Migration: A Marriage of Small API Mapping Models and Large Language Models, https://dl.acm.org/doi/10.1145/3609437.3609466
- Mapping API elements for code migration with vector representations, https://dl.acm.org/doi/10.1145/2889160.2892661

# Making code more testable

## Motivation
- Can LLMs help generating Test codes (Unit tests)
- Can LLMs help in Fuzzing( Talk with stephan about glue code, between Code and fuzzers)

Yet to study much on this side.


# LLMs to migrate code towards an improved structure 

## Motivation:
- To address data quality issues, researchers have developed LLM-assisted code cleaning pipelines that improve code structure and readability, leading to enhanced code generation performance [5].
- GPT models have shown 90% accuracy in identifying Model-View-Whatever (MVW) design patterns using a rule-based system [6].
- Wadhwa et al. (2023) [7] present CORE, a tool using a pair of LLMs to assist developers in resolving code quality issues flagged by static analysis tools. CORE successfully revised 59.2% of Python files and 76.8% of Java files to pass both tool and human scrutiny.

## Current state of research:
- Start with reading the references and snow ball 
- Used in design pattern recognition, Improving code quality, improving readability, etc.
- Frustrated with Code Quality Issues? LLMs can Help!(Paper)

## Resources:
- https://www.ptidej.net/tools/designpatterns/
- https://ieeexplore.ieee.org/document/9463095
- CROP, https://crop-repo.github.io/

## Challenges:
- Is it required? There are many tools that can already do it?
- How do you evaluate if a code meets quality criteria?


[1] Ali, Azad and David T. Smith. “A Debate over the Teaching of a Legacy Programming Language in an Information Technology (IT) Program.” J. Inf. Technol. Educ. Innov. Pract._13 (2014): 111-127.

[2] Ciborowska, Agnieszka et al. “Contemporary COBOL: Developers' Perspectives on Defects and Defect Location.” _ArXiv abs/2105.01830 (2021): n. pag.

[3] X. Han, B. Hua, Y. Wang and Z. Zhang, "RUSTY: Effective C to Rust Conversion via Unstructured Control Specialization," _2022 IEEE 22nd International Conference on Software Quality, Reliability, and Security Companion (QRS-C)_, Guangzhou, China, 2022, pp. 760-761, doi: 10.1109/QRS-C57518.2022.00122.  

[4] Bingzhe Zhou, Xinying Wang, Shengbin Xu, Yuan Yao, Minxue Pan, Feng Xu, and Xiaoxing Ma. 2023. Hybrid API Migration: A Marriage of Small API Mapping Models and Large Language Models. In Proceedings of the 14th Asia-Pacific Symposium on Internetware (Internetware '23). Association for Computing Machinery, New York, NY, USA, 12–21. https://doi.org/10.1145/3609437.3609466

[5] Jain, Naman et al. “LLM-Assisted Code Cleaning For Training Accurate Code Generators.” _ArXiv_ abs/2311.14904 (2023): n. pag.

[6] Jánki, Zoltán Richárd and Vilmos Bilicki. “Rule-Based Architectural Design Pattern Recognition with GPT Models.” _Electronics_ (2023): n. pag.

[7] Wadhwa, Nalin, Jui Pradhan, Atharv Sonwane, Surya Prakash Sahu, Nagarajan Natarajan, Aditya Kanade, Suresh Parthasarathy and Sriram K. Rajamani. “Frustrated with Code Quality Issues? LLMs can Help!” _ArXiv_ abs/2309.12938 (2023): n. pag.