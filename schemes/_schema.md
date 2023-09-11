```mermaid
classDiagram
    Root *-- Author
    Root *-- Parameter
    
    class Root {
        +string description*
        +string title123*
        +string[0..*] subject123*
        +Author[0..*] authors*
        +Parameter[0..*] parameters*
    }
    
    class Author {
        +string name*
        +string affiliation
    }
    
    class Parameter {
        +string key*
        +float value*
    }
    
```