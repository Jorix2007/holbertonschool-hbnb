# High-Level Package Diagram

## Architecture Diagram

```mermaid
classDiagram
    namespace Presentation_Layer {
        class API_Endpoints {
            +UserResource
            +PlaceResource
            +ReviewResource
        }
    }

    namespace Business_Logic_Layer {
        class HBnB_Facade {
            <<Interface>>
            +create_user(data)
            +get_place(id)
            +save_review(data)
        }
        class Models {
            +User
            +Place
            +Review
            +Amenity
        }
    }

    namespace Persistence_Layer {
        class Repository {
            <<Interface>>
            +save(obj)
            +get(id)
            +delete(id)
        }
        class Database {
            +SQLAlchemy
            +FileStorage
        }
    }

    API_Endpoints --> HBnB_Facade : Calls methods
    HBnB_Facade --> Models : Manages entities
    HBnB_Facade --> Repository : Persists data
    Repository --> Database : Executes Queries