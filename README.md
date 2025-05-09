# Plantuml Nord Themes

## Usage

```plantuml
!theme nord-night from https://raw.githubusercontent.com/jason9075/plantuml-nord-themes/main/themes

```

## Example

### Sequence

```plantuml
@startuml
!theme nord-night from https://raw.githubusercontent.com/jason9075/plantuml-nord-themes/main/themes
skinparam actorStyle awesome
title Brother May I Have Some Oats
actor Actor1 as A1
actor Actor2 as A2 $RED
A1 -> A2: Brother, may I have some oats?
A2 -> A1: No.
A1 -> A2: I am straving, brother.
A2 -> A1: As am i, brother.\nThe tall skinny figure has thrown the oats at me.\n<color $RED>**ME! BROTHER**</color>.\nI believe they have taken a liking to me.
@enduml
```

![Sequence](./imgs/sequence.png)

### State

```plantuml
@startuml
!theme nord-night from https://raw.githubusercontent.com/jason9075/plantuml-nord-themes/main/themes
title State Machine Diagram

state NotStarted:
state Waiting: jump to next state by type
state Failed: if process file failed when\nworker just start
state Converting: convert pdf to markdown
state Summarizing: 1.fetch file from minio\n2.use pipeline to gen summary
state Unspecified: may come from any state if\nerror occurs

[*] --> Failed : <color:red> error
[*] --> NotStarted : UploadCatalogFile()
[*] --> Waiting : ProcessKnowledgeBaseFiles()
Waiting --> Converting : pdf,doc,ppt
Waiting --> Summarizing : text,markdown
Converting -r-> Summarizing : markdown
Summarizing --> RAG
state RAG {
    state Chunking:1.fecth file from minio\n2.chunk text pipeline\n3.save and update file
    state Embedding:1.get chunk from db\n2.call embedding pipeline\n3.save embedding to milvus\n4.update files
    state Completed:log info
  [*] --> Chunking
  Chunking --> Embedding
  Embedding --> Completed
}
RAG --> [*]
Unspecified --> [*]
@enduml
```

![State](./imgs/state.png)

## Ref

[Color Ref](https://www.nordtheme.com/)
