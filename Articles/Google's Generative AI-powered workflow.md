https://research.google/blog/accelerating-code-migrations-with-ai/

Google's monorepo is an example of large code datasets, which includes [billions](https://research.google/pubs/why-google-stores-billions-of-lines-of-code-in-a-single-repository/) of lines of code.

Code migration includes: accommodate new language versions, framework updates, changing APIs and data types across this vast codebase.

In the past:
Employed special infrastructure for large scale changes, using static tools like Kythe and Code Search to discover locations, ClangMR to employ changes.

 - Worked well for uniform structure and have limited set of edge cases.
 - Struggles with complex structure. i.e changing interfaces and their usages across multiple components and their dependencies or updating their tests.

Now:
Conceptually split the process of the migration into three stages:

1. Targeting the locations in the codebase that needed modifications
2. Edit generation and validation
3. Change review and rollout

Focus is on #2.

To generate and validate code, used Gemini model, fine tuned with internal Google code and data.

Each migration requires as input:

- A set of files and the locations of expected changes: path + line number in the file
- One or two prompts that describe the change
- [Optional] Few-shot examples to decide if a file actually needs migration

Process:

File Location provided by the user are collected through a combination of pre-existing static tools and human input. Automatically includes additional relevant files test files, interface files, and other dependencies. Uses Cross-reference information not AI.

Thus, to avoid redundant changes or confusing the model during edit generation we provide the model with few-shot examples and ask it to predict if a file needs to be migrated.

Model was trained following the [DIDACT methodology](https://research.google/blog/large-sequence-models-for-software-development-activities/) on data from Google’s [monorepo](https://en.wikipedia.org/wiki/Monorepo) and processes. At inference time, we annotate each line where we expect a change is needed with a natural language instruction as well as a general instruction for the model. In each model query, the input context can contain one or multiple files related to each other.

The model then predicts differences between the files ([diffs](https://en.wikipedia.org/wiki/Diff)) where changes are needed and can also change related sections so that the final code is correct.

This last capability is critical to increase migration velocity, because the generated changes might not be aligned with the initial locations requested, but they will solve the intent. This reduces the need to manually find the full set of lines where changes are needed and is a big step forward compared to purely deterministic change generation based on abstract syntax tree modifications.

Different combinations of prompts yield different results depending on the input context. In some cases providing too many locations where one might expect a change results in worse performance than specifying a change in just one place in the file and prompting the model to apply the change to the file globally.

As we apply changes across dozens and potentially hundreds of files, we implement a mechanism that generates prompt combinations that are tried in parallel for each file group. This is similar to a [pass@k](https://arxiv.org/abs/2107.03374) strategy where instead of [inference temperature](https://www.iguazio.com/glossary/llm-temperature/#:~:text=LLM%20temperature%20is%20a%20parameter,probability%2C%20i.e%20more%20creative%20outputs) we modify the prompting strategy.

Validation:

Validate with compiling the changed files and Unit Test. Optionally repair using AI again. As we generate multiple changes for each file group, we score them based on the validations and at the end decide which set of changes to propagate back to the final change list (similar to a pull request in [Git](https://en.wikipedia.org/wiki/Git)).


Case study: Migrating integers from 32-bit to 64-bit


## Future directions

The next step is addressing more complex migrations that impact multiple components exchanging data or requiring system architecture changes. We have already had success when migrating from deprecated types that require non-trivial refactorings, as well as moving away from older testing frameworks.

We are researching how to apply AI in the other parts of the development journey, specifically to help with targeting the changes and better filtering those that are unnecessary. Another interesting area is to improve the migration user experience in the IDE so that it gives greater control and freedom to the change operator to mix-and-match the existing tooling.

Overall we see a wide potential application of this work, likely beyond the strict space of code migration and possibly also applied to error correction and general code maintenance at scale.