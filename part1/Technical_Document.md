# HBnB Technical Design Document

## 1. Introduction

### Overview
The HBnB project is a full-stack web application that replicates the core functionalities of the AirBnB platform. It allows users to register, create property listings (places), leave reviews, and manage amenities. 

### Purpose of this Document
This technical document serves as a comprehensive blueprint for the architectural design and business logic of the HBnB application. It is intended to guide the engineering team through the implementation phases by providing a clear reference for the system’s architecture, class structures, and interaction flows. By adhering to the designs outlined in this document, the development team ensures a scalable, maintainable, and decoupled codebase.

---

## 2. High-Level Architecture

The HBnB application utilizes a classic Three-Layer Architecture, decoupled through the implementation of the Facade design pattern.

### Package Diagram

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