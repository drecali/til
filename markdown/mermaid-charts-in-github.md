# Mermaid charts in GitHub

[Mermaid charts](https://mermaid-js.github.io/mermaid/) are SVG charts generated from simple markup. They're super useful for displaying logic visually.

## Benefits

- Visual communication can be clearer and easier to understand than written communication, especially for diverse teams with some language barriers.
- Adding visuals to a written explanation is an effective summary.
- Visuals make onboarding much more pleasant.
- A diagram makes it easy to identify bottlenecks, inefficiencies, or other edge cases in processes and situations.

##

I've only used them for `Sequence Diagrams` but it supports many other types of charts like `Flow Charts`, `Class Diagrams`, `State Diagrams`, `User Journeys`, `ER Diagrams`, `Git Graphs`, `Gantt Charts`, and `Pie Charts`.

For a Mermaid charts editor, I recommend [mermaid.live](https://mermaid.live/). It's free and updates in real time. You can create and edit your chart there, then paste it into

There's also a VS Code [extension](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid) but if you type slowly, it will try to render your unfinished input so the integrated preview will look broken until syntax errors are corrected. It works well after you correct syntax errors.

## Use in GitHub

Mermaid charts should be in a Markdown [fenced code block](https://www.markdownguide.org/extended-syntax/#fenced-code-blocks) with `mermaid` as the language for syntax highlighting. The output is an SVG.

### Syntax:

\`\`\`mermaid

{diagramType}

{Mermaid chart code}

\`\`\`

GitHub-flavored Markdown only started supporting Mermaid Charts in 2022. See this [article](https://github.blog/2022-02-14-include-diagrams-markdown-files-mermaid/) for details.

## Sequence Diagrams

```mermaid
sequenceDiagram
  participant User as User
  participant FE as Front End
  participant API as API
    User->>+FE: Submit search query
        FE->>+API: Request search query
        API-->>-FE: Respond with search query results
    FE-->>-User: Show search query results
```

## Flow Chart

```mermaid
graph TD
    A[Christmas] -->|Get money| B(Go shopping)
    B --> C{Let me think}
    C -->|One| D[Laptop]
    C -->|Two| E[iPhone]
    C -->|Three| F[fa:fa-car Car]
```

## Class Diagram

```mermaid
classDiagram
    Animal <|-- Duck
    Animal <|-- Fish
    Animal <|-- Zebra
    Animal : +int age
    Animal : +String gender
    Animal: +isMammal()
    Animal: +mate()
    class Duck{
      +String beakColor
      +swim()
      +quack()
    }
    class Fish{
      -int sizeInFeet
      -canEat()
    }
    class Zebra{
      +bool is_wild
      +run()
    }
```

## State Diagram

```mermaid
stateDiagram-v2
    [*] --> Still
    Still --> [*]
    Still --> Moving
    Moving --> Still
    Moving --> Crash
    Crash --> [*]

```

## User Journeys

```mermaid
  journey
    title My working day
    section Go to work
      Make tea: 5: Me
      Go upstairs: 3: Me
      Do work: 1: Me, Cat
    section Go home
      Go downstairs: 5: Me
      Sit down: 3: Me

```

## ER Diagram

```mermaid
erDiagram
          CUSTOMER }|..|{ DELIVERY-ADDRESS : has
          CUSTOMER ||--o{ ORDER : places
          CUSTOMER ||--o{ INVOICE : "liable for"
          DELIVERY-ADDRESS ||--o{ ORDER : receives
          INVOICE ||--|{ ORDER : covers
          ORDER ||--|{ ORDER-ITEM : includes
          PRODUCT-CATEGORY ||--|{ PRODUCT : contains
          PRODUCT ||--o{ ORDER-ITEM : "ordered in"

```

## Git Graph

```mermaid
gitGraph
    commit
    commit
    branch develop
    checkout develop
    branch feat1
    checkout feat1
    commit
    commit
    checkout develop
    merge feat1
    branch feat2
    checkout feat2
    commit
    checkout develop
    merge feat2
    checkout main
    merge develop
    commit
    commit
```

## Gantt Charts

```mermaid
gantt
    title A Gantt Diagram
    dateFormat  YYYY-MM-DD
    section Section
    A task           :a1, 2014-01-01, 30d
    Another task     :after a1  , 20d
    section Another
    Task in sec      :2014-01-12  , 12d
    another task      : 24d

```

## Pie Chart

```mermaid
pie title Pets adopted by volunteers
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15

```
