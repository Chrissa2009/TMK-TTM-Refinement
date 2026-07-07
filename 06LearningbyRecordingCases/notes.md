# TMK Refinement Notes

## Refinement 1: Compared TMK Model Against Lesson

### Summary
Reviewed the Learning by Recording Cases TMK model against the lesson PDF and identified where the model already aligned with the lecture and where it was still too compressed.

### Covered by the Existing Model

#### Recorded Cases and Case Memory
- The Knowledge model already included `recordedCase`, `newProblem`, and `caseMemory`.
- This matched the lesson's explanation that an agent stores prior cases in memory and uses them to answer new problems.

#### Similarity-Based Retrieval
- The Task and Method models already included `ComputeSimilarity` and `RetrieveNearestCase`.
- This aligned with the lesson's nearest-neighbor framing: find the stored case most similar to the new problem.

#### Feature-Space Representation
- The model included `problemRepresentation` and `distanceSet`.
- This partially captured the lesson's block-world and navigation examples, where problems and cases are represented in a coordinate or multidimensional space.

#### Solution Transfer
- The model included `ApplyCaseSolution`.
- This reflected the basic lesson pattern: retrieve a similar case and apply that case's answer to the current problem.

### Gaps Identified

#### Learning by Recording
- The model emphasized solving by retrieving cases more than learning by recording new cases.
- The lesson frames recording individual prior cases as the learning mechanism that enables future problem solving.

#### Case Structure
- `recordedCase` was present, but the model did not explicitly define the internal parts of a case.
- The lesson implies that a case includes a prior problem, its represented features, and its associated answer or solution.

#### Distance and Dimensionality
- The model referenced distance and nearest-neighbor retrieval, but did not explicitly define `euclideanDistance`, `dimension`, `coordinate`, or `kDimensionalSpace`.
- The lesson spends time generalizing from a two-dimensional block example to a multidimensional navigation example.

#### Adaptation and Evaluation
- The original FSM ended immediately after `ApplyCaseSolution`.
- The lesson explicitly warns that even a very close retrieved case may not have a solution that should be directly applied.
- The lesson also motivates the need for methods that adapt past cases before accepting them.

### Rationale
The initial model captured the core retrieval idea well, but it treated nearest-case retrieval and solution transfer as more complete than the lesson does. The lecture uses nearest neighbor as an important method, then highlights its limits and points toward adaptation and evaluation as necessary extensions.

## Refinement 2: Added Adaptation and Evaluation to the Method

### Summary
Updated the Method model so that retrieving the nearest case and transferring its solution produces a candidate solution, not an automatic final answer.

### Changes

#### Candidate Solution
- Updated `ApplyCaseSolution` so it now produces `candidateConfiguration` rather than `finalConfiguration`.
- This represents the transferred solution from the retrieved case before it has been adapted or accepted.

#### AdaptCaseSolution
- Added the `AdaptCaseSolution` task.
- Added the `AdaptCaseSolutionMechanism` method.
- Added an FSM state after `ApplyCaseSolution` to adapt or confirm the transferred solution for the current problem.

#### EvaluateAdaptation
- Added the `EvaluateAdaptation` task.
- Added the `EvaluateAdaptationMechanism` method.
- Added an FSM state that checks whether the adapted solution is acceptable before the method transitions to completion.

#### Completion Logic
- Changed the FSM success path from:
  `RetrieveNearestCase -> ApplyCaseSolution -> Complete`
- To:
  `RetrieveNearestCase -> ApplyCaseSolution -> AdaptCaseSolution -> EvaluateAdaptation -> Complete`
- The final transition now depends on `acceptableAdaptation(finalConfiguration)`.

#### Failure Logic
- Added failure transitions when the transferred solution cannot be adapted or when the adapted solution is not acceptable.
- This reflects the lesson's warning that similarity alone does not guarantee applicability.

### Rationale
The lesson states that retrieving the nearest case is not always sufficient. Even when a new problem is close to a prior case, the prior solution may not directly fit. Adding adaptation and evaluation keeps the model aligned with that conclusion while still preserving the lesson's simpler nearest-neighbor method as the starting point.

## Refinement 3: Added Knowledge for Adapted Case Use

### Summary
Expanded the Knowledge model to support the new adaptation and evaluation steps in the Method model.

### Changes

#### caseSolution
- Added the `caseSolution` concept.
- Represents the solution associated with a recorded case.

#### candidateSolution
- Added the `candidateSolution` concept.
- Represents a transferred case solution before it has been adapted or accepted.

#### adaptedSolution
- Added the `adaptedSolution` concept.
- Represents a case solution modified or confirmed for the current problem.

#### adaptationEvaluation
- Added the `adaptationEvaluation` concept.
- Represents the assessment of whether an adapted solution fits the new problem.

#### New Relations
- Added `hasSolution` from `recordedCase` to `caseSolution`.
- Added `transfersSolutionTo` from `recordedCase` to `newProblem`.
- Added `adaptsSolutionFor` from `caseSolution` to `newProblem`.
- Added `evaluatesFitFor` from `adaptedSolution` to `newProblem`.

#### New Assertions
- Added `transferredCaseSolution`.
- Added `adaptedCaseSolution`.
- Added `acceptableAdaptation`.
- Updated `goodCaseRetrieval` so it represents retrieved-case solution transfer rather than final success.

### Rationale
The adaptation/evaluation states in the Method model need corresponding Knowledge definitions. These additions distinguish retrieving a similar case, transferring its solution, adapting that solution, and accepting it as appropriate for the new problem. That distinction is central to the lecture's closing point about the limitations of direct nearest-neighbor application.
