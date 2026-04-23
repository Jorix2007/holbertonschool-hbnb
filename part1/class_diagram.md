# Detailed Class Diagram for Business Logic Layer

## UML Class Diagram

```mermaid
classDiagram
    class BaseModel {
        +UUID4 id
        +DateTime created_at
        +DateTime updated_at
        +save()
        +update(data)
    }

    class User {
        +String email
        +String password
        +String first_name
        +String last_name
        +register()
        +update_profile()
    }

    class Place {
        +String title
        +String description
        +Float price_by_night
        +Integer max_guests
        +Float latitude
        +Float longitude
        +UUID4 host_id
        +add_review(review)
        +add_amenity(amenity)
    }

    class Review {
        +String text
        +Float rating
        +UUID4 place_id
        +UUID4 user_id
        +edit_text(new_text)
    }

    class Amenity {
        +String name
        +String description
        +update_name(new_name)
    }

    %% Inheritance (IS-A relationship)
    BaseModel <|-- User
    BaseModel <|-- Place
    BaseModel <|-- Review
    BaseModel <|-- Amenity

    %% Associations (HAS-A relationship)
    User "1" --> "*" Place : Hosts (One-to-Many)
    User "1" --> "*" Review : Writes (One-to-Many)
    Place "1" --> "*" Review : Receives (One-to-Many)
    Place "*" --> "*" Amenity : Has (Many-to-Many)