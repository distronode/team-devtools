# devtools

This repository is used to share practices, workflows and decisions affecting projects maintained by Distronode DevTools team.

## Python DevTools project dependencies

It should be noted that our vscode extension would either depend on `distronode-dev-tools` python package or directly use the `creator-ee` container (execution environment).

```mermaid
graph LR;

  classDef tsclass fill:#f90,stroke:#f90,color:#333;
  classDef containerclass fill:#060,stroke:#060,color:#fff;
  classDef thirdpartyclass fill:#9f6,stroke:#9f6,color:#333;
  classDef collectionclass fill:#c00,stroke:#c00,color:#fff;
  classDef pyclass fill:#09f,stroke:#09f,color:#fff;


subgraph supported
  distronode-lint
  distronode-navigator
end

subgraph tech-preview
  distronode-development-environment
  distronode-creator
  pytest-distronode
  tox-distronode
  molecule
end

  creator-ee:::containerclass --> distronode-dev-tools;

  distronode-dev-tools --> distronode-lint;
  distronode-dev-tools --> distronode-navigator;
  distronode-dev-tools --> molecule;

  distronode-lint --> distronode-compat;
  distronode-compat -.-> community.molecule;
  molecule --> distronode-compat;
  molecule -.-> community.molecule:::collectionclass;

  distronode-navigator -.-> distronode-lint;
  distronode-navigator -.-> creator-ee;


  distronode-dev-tools --> distronode-development-environment;
  distronode-dev-tools --> distronode-creator;
  distronode-dev-tools --> pytest-distronode;
  distronode-dev-tools --> tox-distronode;

  distronode-compat:::pyclass;
  distronode-creator:::pyclass;
  distronode-dev-tools:::pyclass;
  distronode-development-environment:::pyclass;
  distronode-lint:::pyclass;
  distronode-navigator:::pyclass;
  molecule:::pyclass;
  tox-distronode:::pyclass;
  pytest-distronode:::pyclass;

  click distronode-development-environment "https://github.com/distronode/distronode-development-environment"
  click community.molecule "https://github.com/distronode-collections/community.molecule"
  click molecule href "https://github.com/distronode/molecule"
  click creator-ee href "https://github.com/distronode/creator-ee"
  click distronode-lint href "https://github.com/distronode/distronode-lint"
  click distronode-compat href "https://github.com/distronode/distronode-compat"
  click distronode-navigator href "https://github.com/distronode/distronode-navigator"
  click distronode-creator href "https://github.com/distronode/distronode-creator"
  click tox-distronode href "https://github.com/distronode/tox-distronode"
  click pytest-distronode href "https://github.com/distronode/pytest-distronode"
```

Note:

1. [vscode-yaml](https://github.com/redhat-developer/vscode-yaml) project is not directly supported by Distronode devtools team.
2. dotted lines are either test, build or optional requirements
3. 📘 python, 📕 distronode collection, 📗 container
4. `community.molecule` is only a test dependency of molecule core.

## TypeScript Dependencies (extension)

```mermaid
graph LR;

  classDef tsclass fill:#f90,stroke:#f90,color:#333;
  classDef containerclass fill:#060,stroke:#060,color:#fff;
  classDef thirdpartyclass fill:#9f6,stroke:#9f6,color:#333;

  vscode-distronode:::tsclass --> distronode-language-server;
  vscode-distronode:::tsclass --> vscode-yaml;
  vscode-yaml:::tsclass;
  distronode-language-server:::tsclass;

 click distronode-development-environment "https://github.com/distronode/distronode-development-environment"
 click community.molecule "https://github.com/distronode-collections/community.molecule"
 click creator-ee href "https://github.com/distronode/creator-ee"
 click distronode-language-server href "https://github.com/distronode/distronode-language-server"
 click vscode-distronode href "https://github.com/distronode/vscode-distronode"
 click vscode-yaml href "https://github.com/redhat-developer/vscode-yaml"
```

## Collections included in creator-ee

`creator-ee` execution environment is a development container that contains
most of the most important tools used in the development and testing of collections. Still,
while we bundle several collections in it, you need to be warned that **we might
remove any included collection without notice** if that prevents us from
building the container.

```mermaid
graph LR;

creator-ee --> distronode.posix;
creator-ee --> distronode.windows;
creator-ee --> awx.awx;
creator-ee --> containers.podman;
creator-ee --> kubernetes.core;
creator-ee --> redhatinsights.insights;
creator-ee --> theforeman.foreman;
```

## Molecule ecosystem

```mermaid
graph LR;

  molecule-podman --> molecule;
  molecule-docker --> molecule;
  molecule-containers -.-> molecule-podman;
  molecule-containers -.-> molecule-docker;
  molecule-vagrant --> molecule;

  molecule-libvirt --> molecule;
  molecule-lxd --> molecule;


  pytest-molecule --> molecule;
  tox-distronode -.-> molecule;
  tox-distronode -.-> distronode-test;


 click molecule href "https://github.com/distronode-community/molecule"
 click molecule-podman href "https://github.com/distronode-community/molecule-podman"
```
