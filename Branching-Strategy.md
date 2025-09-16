# Branching Strategy

Git is the most widely used open-source version control system that helps developers to manage, track, 
organize, and share their code. It diligently monitors alterations made to the code by developers, fostering 
seamless collaboration and preempting conflicts that may arise when multiple developers collaborate on a 
single project.

## Branching Strategy in Git
Branching stands as a pivotal aspect within Git, affording developers the capacity to establish numerous 
branches, carry out work on them, and subsequently merge them into the main branch. A Branching strategy 
essentially encompasses a collection of guidelines that teams adhere to during the process of writing, 
merging, and deploying their code through a version control tool like Git.

## Need for a Branching Strategy
Merging code can be quite demanding, especially when the entire team is actively engaged in coding. A 
well-devised branching strategy simplifies this undertaking and maintains code integrity, mitigating the 
risk of code errors and conflicts. This strategy establishes a clear framework, outlining rules and workflows
that dictate how developers create branches for new features, new releases and bug fixes. It also covers 
naming conventions and procedures for pulling, pushing, merging, and deploying code.

The good news is that we don't have to start from scratch when it comes to defining these workflows, as they
have already been established and documented.

## Criteria for determining a branching strategy

| # | Criteria                        | Value |
|---|---------------------------------|-------|
| 1 | Team size                       |       |
| 2 | Stability of the release        |  Yes  |
| 3 | Support Multiple versions       |  Yes  |
| 4 | Parallel releases               |  Yes  |
| 5 | Frequency of releases           |       |
| 6 | Maintenance overhead (branches) |       |
| 7 | Testing automation maturity     |  Yes  |
| 8 | Continuous delivery/deployment  |  Yes  |
| 9 | Packaged Product vs Application |       |


## Maturity Ladder
The branching strategy follows 4 levels of maturity, each with specific practices and goals. Teams will start at Level 4 and progress through the stages until they reach Level 1.This approach encourages incremental adoption that enhances software quality, deployment efficiency and overall team productivity.

> Level 4 : CI builds - Baseline version control with consistent builds

At this stage the focus is on laying a foundation for version control practices with Gitflow and CI pipelines.

Requirement
- Gitflow branching mode
- Consistent branch naming
- Reproducible builds

Evaluation
- Single repository
- CI setup
- Versioned build artifact (using semantic versioning - Major.Minor.Patch)

Recreating a build
What is needed?

|# | Tooling        | Required      | Comments  |
|--|----------------|---------------|-----------|
|1 | Version Control System | Y | Use Git to track code changes and version |
|2 | Dependency management | Y | Tools like Maven or NPM |
|3 | Build automation | Y | Tools like Jenkins, GitHub Actions |
|4 | Artifact Repository | Y | Artifactory or Nexus |
|5 | Checksum verification | Y | Implement checksums or hashes to verify the integrity |
|6 | Configuration versions | Y | Changes or drift in application config files |
|7 | Network dependencies | Y | Reliance on external newtwork resources |
|8 | Containerization | N | Docker or similar tools | 
|9 | Configuration management | N | Tools like Ansible, Puppet or Chef |
|10 | IaC | Tools like Terraform or CloudFormation | 
|11 | Tooling Versions | N | Same version of build tools to product same output | 
|12 | Environment drift | N | Changes in environment variables that impact build |

> Level 3 : CI - Maintain a Green Develop branch with deployable state

Requirement

- Same as Level 4

Evaluation

- Github flow branching strategy is employed for the repo, removing the need for long lived release branches
- TDD with unit testing, virtualized component testing, static analysis and contract test
- Code Reviews before merge to Develop
- CI quality gate enforcement
- Short lived feature branches
- Regular green build validation to ensure that develop is always in a deployable state
- Effective CI monitoring

> Level 2 : Basic CD (deployment) always ready to deploy to PROD with feature flags

Requirement

- Same as Level 3

Evaluation

- Trunk based or scaled trunk based, removing the need for develop branch. Short lived release branches for deployment
- Regular automated deploy to PROD within 2 days of sprint close
- Automated acceptance and regression testing
- Comprehensive test automation
- CD quality gate enforcement
- Validate all changes in a E2E Pre-Prod environment


> Level 1 : Single codebase with CD (Delivery) to PROD using Trunk based development

Requirement

- Same as Level 3

Evaluation

- Feature flagging
- Fully automated CD to PROD
- Post Deployment Verification
- Automated Rollback
- Audited Deployments


> Option 1: Based on the above criteria, `GitFlow` is the branching strategy of choice since there is a need to support multiple versions and parallel releases. The details below depicts the developer journey as a part of every sprint.

Assumption
- Branching strategy will be owned by Engineering teams
- CI pipeline will be defined by Engineering teams
- CI tollgates are defined and controlled by Engineering teams with evidence produced to Release Engineering
- CI phase will produce the necessary binary artifacts to the binary repository (e.g., Artifactory)

BUILD PHASE - CI Pipeline

- Code is compiled
- Run unit, component and contract tests
- No tollgate checks
- Binary artifact is generated

INTEGRATION PHASE - CI Pipeline

- Code is compiled
- Run unit, component and contract tests
- Security scans
- All tollgate checks are enforced
- Binary artifact is generated

INTEGRATION PHASE - CD Pipeline

- Code is deployed to Integration environment
- Run Acceptance Test and Performance Test

[Click here to view the Gitflow Scenarios](../excalidraw/ci-cd/gitflow-pipeline.excalidraw)

> Option 2: Trunk based development with feature flags

When deciding between trunk based and scaled trunk based, team size plays a major role. Trunk based development is ideal for smaller teams (5-8 developers), where developers can frequently integrate changes in a single trunk, ensuring CI and minimizing merge conflicts. This approach fosters rapid feedback and agility, making it suitable for teams that can maintain close communication. On the other hand scaled trunk based is suited for larger teams or places where multiple feature branches are necessary to manage parallel development efforts. This strategy allows for short-lived feature branches that undergo rigorous code reviews and automated testing before merging into the trunk, providing a balance of flexibility and stability. The decision between these strategies depends on the team's capacity to handle integration complexity and sustain efficient collaboration. 



## Anti patterns

- Not following Gitflow or Github branching strategy or violating branching rules
    - Branching should only occur from Trunk, develop or release branches
    - Feature branches must not be created off other feature or hotfix branches
    - Fixes to the release branch must be automatically down-merged to Develop
    - The only long-lived branches are trunk and develop
- Unambiguous code representation
    - There must be a clear and unambiguous representation of the code currently in Prod that can be recreated
    - A clear branch, typically Develop should contain the Green build that is ready for deployment
- Single Repository for Deployable components
    - A deployable component should reside in a single repository
    - The use of separate repos for things like Release or Test is a anti pattern
- No pipelines established
    - A CI pipeline must be established to automate build process
    - Lack of a CI pipeline will result in manual process
- Using snapshots or not pinning dependencies to build deployed code
    - Using snapshot versions for building deployed code is an anti pattern
    - Snapshots are mutable and can change over time
    - Builds should use fixed, versioned dependencies
    - Builds should be labelled